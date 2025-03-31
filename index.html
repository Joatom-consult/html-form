<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Submission System</title>
    <style>
        /* Reset and base styles */
        *, *::before, *::after {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            background-color: #f9fafb;
            color: #374151;
            line-height: 1.5;
        }
        
        /* Container styles */
        .container {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }
        
        .form-card {
            width: 100%;
            max-width: 36rem;
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            padding: 1.5rem;
        }
        
        @media (min-width: 768px) {
            .form-card {
                padding: 2rem;
            }
        }
        
        /* Header styles */
        .form-header {
            margin-bottom: 2rem;
            text-align: center;
        }
        
        .form-header h1 {
            font-size: 1.5rem;
            font-weight: 600;
            color: #1f2937;
            margin-bottom: 0.5rem;
        }
        
        .form-header p {
            color: #6b7280;
        }
        
        .submission-count {
            display: inline-flex;
            align-items: center;
            background-color: #e0f2fe;
            color: #0369a1;
            font-size: 0.75rem;
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            margin-top: 0.5rem;
        }
        
        /* Form styles */
        .form-section {
            margin-bottom: 1.5rem;
        }
        
        .section-title {
            font-size: 1.125rem;
            font-weight: 500;
            border-bottom: 1px solid #e5e7eb;
            padding-bottom: 0.5rem;
            margin-bottom: 1rem;
        }
        
        .form-grid {
            display: grid;
            gap: 1rem;
        }
        
        @media (min-width: 768px) {
            .form-grid-2 {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        
        .form-group {
            position: relative;
            margin-bottom: 0.5rem;
        }
        
        .form-label {
            display: block;
            font-size: 0.875rem;
            font-weight: 500;
            color: #4b5563;
            margin-bottom: 0.25rem;
        }
        
        .form-control {
            display: block;
            width: 100%;
            padding: 0.75rem 0.75rem;
            font-size: 0.875rem;
            font-weight: 400;
            line-height: 1.5;
            color: #374151;
            background-color: #fff;
            background-clip: padding-box;
            border: 1px solid #d1d5db;
            border-radius: 0.375rem;
            transition: border-color 0.15s ease-in-out;
        }
        
        .form-control:focus {
            border-color: #2563eb;
            outline: 0;
        }
        
        .form-control.error {
            border-color: #ef4444;
        }
        
        .error-message {
            display: block;
            color: #ef4444;
            font-size: 0.75rem;
            margin-top: 0.25rem;
        }
        
        /* Radio button styles */
        .radio-group {
            margin-top: 0.5rem;
        }
        
        .radio-container {
            display: grid;
            grid-template-columns: repeat(1, 1fr);
            gap: 0.5rem;
        }
        
        @media (min-width: 640px) {
            .radio-container {
                grid-template-columns: repeat(2, 1fr);
            }
        }
        
        .radio-option {
            display: flex;
            align-items: center;
        }
        
        .radio-input {
            height: 1rem;
            width: 1rem;
            color: #2563eb;
            border-color: #d1d5db;
            border-radius: 50%;
        }
        
        .radio-label {
            margin-left: 0.5rem;
            font-size: 0.875rem;
            color: #4b5563;
        }
        
        /* Button styles */
        .btn {
            display: inline-flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            padding: 0.625rem 1rem;
            background-color: #2563eb;
            color: white;
            font-weight: 500;
            font-size: 0.875rem;
            line-height: 1.5;
            border-radius: 0.375rem;
            border: none;
            cursor: pointer;
            transition: background-color 0.15s ease-in-out;
        }
        
        .btn:hover {
            background-color: #1d4ed8;
        }
        
        .btn:disabled {
            opacity: 0.7;
            cursor: not-allowed;
        }
        
        .spinner {
            display: inline-block;
            margin-left: 0.5rem;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            from {
                transform: rotate(0deg);
            }
            to {
                transform: rotate(360deg);
            }
        }
        
        /* Footer styles */
        .form-footer {
            margin-top: 1.5rem;
            text-align: center;
            font-size: 0.875rem;
            color: #6b7280;
        }
        
        /* Toast notification styles */
        .toast {
            position: fixed;
            top: 1.25rem;
            right: 1.25rem;
            max-width: 20rem;
            width: 100%;
            padding: 1rem;
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            display: flex;
            align-items: center;
            z-index: 50;
            opacity: 0;
            transform: translateY(-1rem);
            transition: opacity 0.3s ease, transform 0.3s ease;
        }
        
        .toast.show {
            opacity: 1;
            transform: translateY(0);
        }
        
        .toast-success {
            border-left: 4px solid #10b981;
        }
        
        .toast-error {
            border-left: 4px solid #ef4444;
        }
        
        .toast-icon {
            margin-right: 0.75rem;
            font-size: 1.25rem;
        }
        
        .toast-success .toast-icon {
            color: #10b981;
        }
        
        .toast-error .toast-icon {
            color: #ef4444;
        }
        
        .toast-content {
            flex: 1;
        }
        
        .toast-title {
            font-weight: 500;
            color: #1f2937;
        }
        
        .toast-message {
            font-size: 0.875rem;
            color: #6b7280;
        }
        
        .toast-close {
            background: transparent;
            border: none;
            color: #9ca3af;
            cursor: pointer;
            margin-left: auto;
            font-size: 1.25rem;
        }
        
        .toast-close:hover {
            color: #6b7280;
        }

        /* Floating label input styles */
        .floating-label-input {
            position: relative;
        }

        .floating-label-input input {
            height: 3.5rem;
            padding-top: 1.25rem;
        }

        .floating-label-input label {
            position: absolute;
            top: 0.5rem;
            left: 0.75rem;
            font-size: 0.75rem;
            color: #6b7280;
            pointer-events: none;
        }
    </style>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>
    <div class="container">
        <div class="form-card">
            <!-- Form Header -->
            <div class="form-header">
                <h1>Submit Your Information</h1>
                <p>Complete the form below to register your details</p>
                <div id="submissionCount" class="submission-count" style="display: none;">
                    <span class="material-icons" style="font-size: 0.875rem; margin-right: 0.25rem;">analytics</span>
                    <span>0 submissions this month</span>
                </div>
            </div>
            
            <!-- Form -->
            <form id="submissionForm">
                <!-- Contact Information Section -->
                <div class="form-section">
                    <h2 class="section-title">Contact Information</h2>
                    
                    <div class="form-grid form-grid-2">
                        <!-- Name Field -->
                        <div class="form-group floating-label-input">
                            <input type="text" id="name" name="name" class="form-control" placeholder=" " required>
                            <label for="name">Full Name</label>
                            <span id="nameError" class="error-message"></span>
                        </div>
                        
                        <!-- Email Field -->
                        <div class="form-group floating-label-input">
                            <input type="email" id="email" name="email" class="form-control" placeholder=" " required>
                            <label for="email">Email Address</label>
                            <span id="emailError" class="error-message"></span>
                        </div>
                    </div>
                    
                    <div class="form-grid">
                        <!-- Phone Field -->
                        <div class="form-group floating-label-input">
                            <input type="tel" id="phone" name="phone" class="form-control" placeholder=" ">
                            <label for="phone">Phone Number</label>
                            <span id="phoneError" class="error-message"></span>
                        </div>
                    </div>
                </div>
                
                <!-- Source Information Section -->
                <div class="form-section">
                    <div class="form-group">
                        <label class="form-label">How did you hear about us?</label>
                        <div class="radio-group">
                            <div class="radio-container">
                                <div class="radio-option">
                                    <input type="radio" id="source-search" name="source" value="search" class="radio-input">
                                    <label for="source-search" class="radio-label">Search Engine</label>
                                </div>
                                <div class="radio-option">
                                    <input type="radio" id="source-social" name="source" value="social" class="radio-input">
                                    <label for="source-social" class="radio-label">Social Media</label>
                                </div>
                                <div class="radio-option">
                                    <input type="radio" id="source-friend" name="source" value="friend" class="radio-input">
                                    <label for="source-friend" class="radio-label">Friend/Referral</label>
                                </div>
                                <div class="radio-option">
                                    <input type="radio" id="source-other" name="source" value="other" class="radio-input">
                                    <label for="source-other" class="radio-label">Other</label>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- Form Submission Section -->
                <div class="form-group">
                    <button type="submit" id="submitButton" class="btn">
                        <span id="submitText">Submit Information</span>
                        <span id="submitSpinner" class="spinner material-icons" style="display: none;">autorenew</span>
                    </button>
                </div>
            </form>
            
            <!-- Form Footer -->
            <div class="form-footer">
                <p>Your information is securely stored and will not be shared with third parties.</p>
            </div>
        </div>
        
        <!-- Toast Notification -->
        <div id="toast" class="toast">
            <span id="toastIcon" class="toast-icon material-icons"></span>
            <div class="toast-content">
                <h3 id="toastTitle" class="toast-title"></h3>
                <p id="toastMessage" class="toast-message"></p>
            </div>
            <button id="toastClose" class="toast-close material-icons">close</button>
        </div>
    </div>

    <script>
        // Google Sheets script URL
        const scriptURL = "https://script.google.com/macros/s/AKfycbxa6h-cJ6HaOP7oyg9xva0_ZGtEdiGwYExyQYdrb7bVGFlfHlucUKA2RZHhOGoo6SNSnQ/exec";
        
        // DOM Elements
        const form = document.getElementById('submissionForm');
        const submitButton = document.getElementById('submitButton');
        const submitText = document.getElementById('submitText');
        const submitSpinner = document.getElementById('submitSpinner');
        const toast = document.getElementById('toast');
        const toastIcon = document.getElementById('toastIcon');
        const toastTitle = document.getElementById('toastTitle');
        const toastMessage = document.getElementById('toastMessage');
        const toastClose = document.getElementById('toastClose');
        const submissionCountContainer = document.getElementById('submissionCount');
        
        // Form field elements and errors
        const nameInput = document.getElementById('name');
        const emailInput = document.getElementById('email');
        const phoneInput = document.getElementById('phone');
        const nameError = document.getElementById('nameError');
        const emailError = document.getElementById('emailError');
        const phoneError = document.getElementById('phoneError');
        
        // Fetch submission count
        async function fetchSubmissionCount() {
            try {
                // For demonstration only - in a real implementation, you would have an API endpoint
                // that returns the actual count from your database
                const count = 0; // Example count
                
                if (count > 0) {
                    submissionCountContainer.querySelector('span:last-child').textContent = `${count} submissions this month`;
                    submissionCountContainer.style.display = 'inline-flex';
                }
            } catch (error) {
                console.error('Error fetching submission count:', error);
            }
        }
        
        // Show toast notification
        function showToast(type, message) {
            // Set toast type
            toast.className = type === 'success' ? 'toast toast-success show' : 'toast toast-error show';
            
            // Set toast icon
            toastIcon.textContent = type === 'success' ? 'check_circle' : 'error';
            
            // Set toast title
            toastTitle.textContent = type === 'success' ? 'Success!' : 'Error';
            
            // Set toast message
            toastMessage.textContent = message || (type === 'success' 
                ? 'Your information has been submitted successfully.' 
                : 'There was a problem submitting your information. Please try again.');
            
            // Show toast
            toast.classList.add('show');
            
            // Auto hide after 5 seconds
            setTimeout(() => {
                hideToast();
            }, 5000);
        }
        
        // Hide toast notification
        function hideToast() {
            toast.classList.remove('show');
        }
        
        // Validate form fields
        function validateForm() {
            let isValid = true;
            
            // Reset errors
            nameError.textContent = '';
            emailError.textContent = '';
            phoneError.textContent = '';
            nameInput.classList.remove('error');
            emailInput.classList.remove('error');
            phoneInput.classList.remove('error');
            
            // Validate name
            if (!nameInput.value.trim()) {
                nameError.textContent = 'Name is required';
                nameInput.classList.add('error');
                isValid = false;
            } else if (nameInput.value.trim().length < 2) {
                nameError.textContent = 'Name must be at least 2 characters';
                nameInput.classList.add('error');
                isValid = false;
            }
            
            // Validate email
            if (!emailInput.value.trim()) {
                emailError.textContent = 'Email is required';
                emailInput.classList.add('error');
                isValid = false;
            } else {
                const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
                if (!emailRegex.test(emailInput.value.trim())) {
                    emailError.textContent = 'Please enter a valid email address';
                    emailInput.classList.add('error');
                    isValid = false;
                }
            }
            
            return isValid;
        }
        
        // Handle form submission
        async function handleSubmit(event) {
            event.preventDefault();
            
            // Validate form
            if (!validateForm()) {
                return;
            }
            
            // Show loading state
            submitButton.disabled = true;
            submitText.textContent = 'Submitting...';
            submitSpinner.style.display = 'inline-block';
            
            try {
                // Create FormData
                const formData = new FormData(form);
                
                // Send data to Google Sheets
                const response = await fetch(scriptURL, {
                    method: 'POST',
                    body: formData
                });
                
                if (response.ok) {
                    // Reset form
                    form.reset();
                    
                    // Show success toast
                    showToast('success');
                    
                    // Update submission count (optional)
                    fetchSubmissionCount();
                } else {
                    // Show error toast
                    showToast('error');
                }
            } catch (error) {
                console.error('Error submitting form:', error);
                showToast('error', 'An unexpected error occurred. Please try again.');
            } finally {
                // Reset loading state
                submitButton.disabled = false;
                submitText.textContent = 'Submit Information';
                submitSpinner.style.display = 'none';
            }
        }
        
        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            // Fetch submission count
            fetchSubmissionCount();
            
            // Set up form submission
            form.addEventListener('submit', handleSubmit);
            
            // Set up toast close button
            toastClose.addEventListener('click', hideToast);
            
            // Set up field validation on blur
            nameInput.addEventListener('blur', function() {
                if (!this.value.trim()) {
                    nameError.textContent = 'Name is required';
                    this.classList.add('error');
                } else if (this.value.trim().length < 2) {
                    nameError.textContent = 'Name must be at least 2 characters';
                    this.classList.add('error');
                } else {
                    nameError.textContent = '';
                    this.classList.remove('error');
                }
            });
            
            emailInput.addEventListener('blur', function() {
                if (!this.value.trim()) {
                    emailError.textContent = 'Email is required';
                    this.classList.add('error');
                } else {
                    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
                    if (!emailRegex.test(this.value.trim())) {
                        emailError.textContent = 'Please enter a valid email address';
                        this.classList.add('error');
                    } else {
                        emailError.textContent = '';
                        this.classList.remove('error');
                    }
                }
            });
        });
    </script>
</body>
</html>
