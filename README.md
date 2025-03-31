import { useQuery } from "@tanstack/react-query";
import { useState, useEffect } from "react";

export default function FormHeader() {
  const [count, setCount] = useState<number | null>(null);

  const { data, isLoading } = useQuery({
    queryKey: ["/api/submission-count"],
    staleTime: 60000, // 1 minute
  });

  useEffect(() => {
    if (data && data.count !== undefined) {
      setCount(data.count);
    }
  }, [data]);

  return (
    <div className="mb-8 text-center">
      <h1 className="text-2xl font-semibold text-gray-800 mb-2">Submit Your Information</h1>
      <p className="text-gray-600">Complete the form below to register your details</p>
      
      {count !== null && !isLoading && (
        <div className="flex justify-center mt-2">
          <span className="inline-flex items-center bg-blue-100 text-blue-800 text-xs px-2.5 py-0.5 rounded-full">
            <span className="material-icons text-xs mr-1">analytics</span>
            <span>{count} submissions this month</span>
          </span>
        </div>
      )}
    </div>
  );
}

      import { useQuery } from "@tanstack/react-query";
import { useState, useEffect } from "react";

export default function FormHeader() {
  const [count, setCount] = useState<number | null>(null);

  const { data, isLoading } = useQuery({
    queryKey: ["/api/submission-count"],
    staleTime: 60000, // 1 minute
  });

  useEffect(() => {
    if (data && data.count !== undefined) {
      setCount(data.count);
    }
  }, [data]);

  return (
    <div className="mb-8 text-center">
      <h1 className="text-2xl font-semibold text-gray-800 mb-2">Submit Your Information</h1>
      <p className="text-gray-600">Complete the form below to register your details</p>
      
      {count !== null && !isLoading && (
        <div className="flex justify-center mt-2">
          <span className="inline-flex items-center bg-blue-100 text-blue-800 text-xs px-2.5 py-0.5 rounded-full">
            <span className="material-icons text-xs mr-1">analytics</span>
            <span>{count} submissions this month</span>
          </span>
        </div>
      )}
    </div>
  );
}
import React, { useState } from "react";
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { formSubmissionSchema, type FormSubmissionInput } from "@shared/schema";
import { apiRequest } from "@/lib/queryClient";
import { validateField } from "@/lib/form-validation";

interface SheetSubmissionFormProps {
  scriptURL: string;
  onSubmitSuccess: () => void;
  onSubmitError: (message: string) => void;
}

export default function SheetSubmissionForm({
  scriptURL,
  onSubmitSuccess,
  onSubmitError,
}: SheetSubmissionFormProps) {
  const [isSubmitting, setIsSubmitting] = useState(false);
  
  const {
    register,
    handleSubmit,
    reset,
    formState: { errors },
  } = useForm<FormSubmissionInput>({
    resolver: zodResolver(formSubmissionSchema),
    defaultValues: {
      name: "",
      email: "",
      phone: "",
      source: "",
    },
  });

  const onSubmit = async (data: FormSubmissionInput) => {
    setIsSubmitting(true);
    
    try {
      // Create FormData object for Google Apps Script
      const formData = new FormData();
      Object.entries(data).forEach(([key, value]) => {
        if (value) {
          if (Array.isArray(value)) {
            formData.append(key, value.join(', '));
          } else {
            formData.append(key, value.toString());
          }
        }
      });
      
      // Send directly to Google Apps Script
      const response = await fetch(scriptURL, {
        method: 'POST',
        body: formData
      });
      
      if (response.ok) {
        reset(); // Reset form
        onSubmitSuccess();
        
        // Also save to our backend for tracking
        try {
          await apiRequest("POST", "/api/submit-form", data);
        } catch (err) {
          console.log("Backend storage error (non-critical):", err);
        }
      } else {
        onSubmitError("Failed to submit form to Google Sheets");
      }
    } catch (error) {
      console.error("Form submission error:", error);
      onSubmitError("An unexpected error occurred. Please try again.");
    } finally {
      setIsSubmitting(false);
    }
  };

  return (
    <form className="space-y-6" onSubmit={handleSubmit(onSubmit)}>
      {/* Personal Information Section */}
      <div className="space-y-4">
        <h2 className="text-lg font-medium border-b pb-2">Contact Information</h2>
        
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
          {/* Name Field */}
          <div className="floating-label-input">
            <input
              type="text"
              id="name"
              className={`w-full rounded-md border ${errors.name ? 'border-error' : 'border-gray-300'} focus:border-primary bg-white px-3 text-gray-800 h-14 pt-4`}
              placeholder=" "
              {...register("name", {
                onBlur: (e) => validateField(e.target, "name", errors),
              })}
            />
            <label htmlFor="name" className="text-gray-600 text-sm">Full Name</label>
            {errors.name && (
              <p className="text-error text-xs mt-1">{errors.name.message}</p>
            )}
          </div>
          
          {/* Email Field */}
          <div className="floating-label-input">
            <input
              type="email"
              id="email"
              className={`w-full rounded-md border ${errors.email ? 'border-error' : 'border-gray-300'} focus:border-primary bg-white px-3 text-gray-800 h-14 pt-4`}
              placeholder=" "
              {...register("email", {
                onBlur: (e) => validateField(e.target, "email", errors),
              })}
            />
            <label htmlFor="email" className="text-gray-600 text-sm">Email Address</label>
            {errors.email && (
              <p className="text-error text-xs mt-1">{errors.email.message}</p>
            )}
          </div>
        </div>
        
        <div className="grid grid-cols-1 gap-4">
          {/* Phone Field */}
          <div className="floating-label-input">
            <input
              type="tel"
              id="phone"
              className={`w-full rounded-md border ${errors.phone ? 'border-error' : 'border-gray-300'} focus:border-primary bg-white px-3 text-gray-800 h-14 pt-4`}
              placeholder=" "
              {...register("phone")}
            />
            <label htmlFor="phone" className="text-gray-600 text-sm">Phone Number</label>
            {errors.phone && (
              <p className="text-error text-xs mt-1">{errors.phone.message}</p>
            )}
          </div>
        </div>
      </div>
      
      {/* How did you hear about us */}
      <div className="space-y-4">
        <div className="space-y-2">
          <label className="text-sm font-medium text-gray-700">How did you hear about us?</label>
          <div className="grid grid-cols-1 sm:grid-cols-2 gap-2">
            <div className="flex items-center">
              <input
                id="source-search"
                type="radio"
                value="search"
                className="h-4 w-4 text-primary border-gray-300 focus:ring-primary"
                {...register("source")}
              />
              <label htmlFor="source-search" className="ml-2 text-sm text-gray-700">Search Engine</label>
            </div>
            <div className="flex items-center">
              <input
                id="source-social"
                type="radio"
                value="social"
                className="h-4 w-4 text-primary border-gray-300 focus:ring-primary"
                {...register("source")}
              />
              <label htmlFor="source-social" className="ml-2 text-sm text-gray-700">Social Media</label>
            </div>
            <div className="flex items-center">
              <input
                id="source-friend"
                type="radio"
                value="friend"
                className="h-4 w-4 text-primary border-gray-300 focus:ring-primary"
                {...register("source")}
              />
              <label htmlFor="source-friend" className="ml-2 text-sm text-gray-700">Friend/Referral</label>
            </div>
            <div className="flex items-center">
              <input
                id="source-other"
                type="radio"
                value="other"
                className="h-4 w-4 text-primary border-gray-300 focus:ring-primary"
                {...register("source")}
              />
              <label htmlFor="source-other" className="ml-2 text-sm text-gray-700">Other</label>
            </div>
          </div>
        </div>
      </div>
      
      {/* Form Submission Section */}
      <div className="pt-2">
        <button
          type="submit"
          disabled={isSubmitting}
          className="w-full bg-primary hover:bg-accent text-white font-medium py-2.5 px-4 rounded-md transition duration-150 ease-in-out flex justify-center disabled:opacity-70"
        >
          <span>{isSubmitting ? "Submitting..." : "Submit Information"}</span>
          {isSubmitting && (
            <span className="material-icons spinner ml-2">autorenew</span>
          )}
        </button>
      </div>
    </form>
  );
}
import React from "react";

interface ToastNotificationProps {
  type: "success" | "error";
  message?: string;
  onClose: () => void;
}

export default function ToastNotification({
  type,
  message,
  onClose,
}: ToastNotificationProps) {
  const isSuccess = type === "success";
  
  return (
    <div className="fixed top-5 right-5 toast shadow-lg rounded-lg p-4 max-w-sm w-full bg-white border-l-4 z-50 flex items-center" 
         style={{
           borderLeftColor: isSuccess ? "#10B981" : "#EF4444",
         }}>
      <div className="flex items-center">
        <span className="material-icons mr-3" style={{ color: isSuccess ? "#10B981" : "#EF4444" }}>
          {isSuccess ? "check_circle" : "error"}
        </span>
        <div>
          <h3 className="font-medium text-gray-900">{isSuccess ? "Success!" : "Error"}</h3>
          <p className="text-sm text-gray-600">
            {isSuccess
              ? message || "Your information has been submitted successfully."
              : message || "There was a problem submitting your information. Please try again."}
          </p>
        </div>
      </div>
      <button className="ml-auto text-gray-400 hover:text-gray-500" onClick={onClose}>
        <span className="material-icons">close</span>
      </button>
    </div>
  );
}
import { pgTable, text, serial, integer, boolean, timestamp } from "drizzle-orm/pg-core";
import { createInsertSchema } from "drizzle-zod";
import { z } from "zod";

export const users = pgTable("users", {
  id: serial("id").primaryKey(),
  username: text("username").notNull().unique(),
  password: text("password").notNull(),
});

export const insertUserSchema = createInsertSchema(users).pick({
  username: true,
  password: true,
});

export type InsertUser = z.infer<typeof insertUserSchema>;
export type User = typeof users.$inferSelect;

// Form submission schema
export const formSubmissions = pgTable("form_submissions", {
  id: serial("id").primaryKey(),
  name: text("name").notNull(),
  email: text("email").notNull(),
  phone: text("phone"),
  birthdate: text("birthdate"),
  occupation: text("occupation"),
  region: text("region"),
  comments: text("comments"),
  interests: text("interests"), // Stored as comma-separated values
  source: text("source"),
  submittedAt: timestamp("submitted_at").notNull().defaultNow(),
});

export const insertFormSubmissionSchema = createInsertSchema(formSubmissions).omit({
  id: true,
  submittedAt: true,
});

export const formSubmissionSchema = z.object({
  name: z.string().min(2, "Name must be at least 2 characters"),
  email: z.string().email("Please enter a valid email address"),
  phone: z.string().optional().or(z.literal("")),
  source: z.string().optional().or(z.literal("")),
  // Keep these fields in the schema but mark as optional
  birthdate: z.string().optional().or(z.literal("")),
  occupation: z.string().optional().or(z.literal("")),
  region: z.string().optional().or(z.literal("")),
  comments: z.string().optional().or(z.literal("")),
  interests: z.array(z.string()).optional(),
});

export type InsertFormSubmission = z.infer<typeof insertFormSubmissionSchema>;
export type FormSubmission = typeof formSubmissions.$inferSelect;
export type FormSubmissionInput = z.infer<typeof formSubmissionSchema>;

    import type { Express } from "express";
import { createServer, type Server } from "http";
import { storage } from "./storage";
import { formSubmissionSchema } from "@shared/schema";
import { ZodError } from "zod";

export async function registerRoutes(app: Express): Promise<Server> {
  // API endpoint to submit form data to Google Sheets
  app.post("/api/submit-form", async (req, res) => {
    try {
      // Validate form data
      const formData = formSubmissionSchema.parse(req.body);
      
      // Transform interests array to string for storage
      const interestsString = formData.interests?.join(",") || "";
      
      // Store submission in our database
      await storage.createFormSubmission({
        name: formData.name,
        email: formData.email,
        phone: formData.phone || "",
        birthdate: formData.birthdate || "",
        occupation: formData.occupation || "",
        region: formData.region || "",
        comments: formData.comments || "",
        interests: interestsString,
        source: formData.source || "",
      });

      // Proxy to Google Sheets via fetch
      const scriptURL = process.env.GOOGLE_SHEETS_SCRIPT_URL || 
        "https://script.google.com/macros/s/AKfycbyJv7BC8M0xy3wTi3ILlYRrsgDgRtCRjfBzHV_JqqoLQRH0x4XlO_B2vWmUcpvCspGoCw/exec";
      
      // Create FormData for Google Sheets API
      const formDataForSheets = new URLSearchParams();
      formDataForSheets.append("name", formData.name);
      formDataForSheets.append("email", formData.email);
      if (formData.phone) formDataForSheets.append("phone", formData.phone);
      if (formData.birthdate) formDataForSheets.append("birthdate", formData.birthdate);
      if (formData.occupation) formDataForSheets.append("occupation", formData.occupation);
      if (formData.region) formDataForSheets.append("region", formData.region);
      if (formData.comments) formDataForSheets.append("comments", formData.comments);
      if (formData.interests) formDataForSheets.append("interests", formData.interests.join(","));
      if (formData.source) formDataForSheets.append("source", formData.source);
      
      // Send data to Google Sheets
      const response = await fetch(scriptURL, {
        method: "POST",
        body: formDataForSheets,
        headers: {
          "Content-Type": "application/x-www-form-urlencoded",
        },
      });
      
      if (!response.ok) {
        throw new Error("Failed to submit to Google Sheets");
      }
      
      res.status(200).json({ success: true, message: "Form submitted successfully" });
    } catch (error) {
      if (error instanceof ZodError) {
        res.status(400).json({ 
          success: false, 
          message: "Validation error", 
          errors: error.errors 
        });
      } else {
        console.error("Form submission error:", error);
        res.status(500).json({ 
          success: false, 
          message: "An error occurred while submitting the form" 
        });
      }
    }
  });

  // API endpoint to get submission count
  app.get("/api/submission-count", async (req, res) => {
    try {
      const count = await storage.getSubmissionCount();
      res.status(200).json({ count });
    } catch (error) {
      console.error("Error getting submission count:", error);
      res.status(500).json({ 
        success: false, 
        message: "Failed to get submission count" 
      });
    }
  });

  const httpServer = createServer(app);

  return httpServer;
}

    import { Switch, Route } from "wouter";
import { queryClient } from "./lib/queryClient";
import { QueryClientProvider } from "@tanstack/react-query";
import { Toaster } from "@/components/ui/toaster";
import NotFound from "@/pages/not-found";
import Home from "@/pages/home";

function Router() {
  return (
    <Switch>
      <Route path="/" component={Home}/>
      <Route component={NotFound} />
    </Switch>
  );
}

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Router />
      <Toaster />
    </QueryClientProvider>
  );
}

export default App;
import FormContainer from "@/components/form-submission/form-container";

export default function Home() {
  return (
    <div className="min-h-screen bg-gray-50 font-sans">
      <FormContainer />
    </div>
  );
}
