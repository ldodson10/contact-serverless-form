# Serverless Contact Form with AWS

This project documents the setup, testing, and deployment of a **serverless contact form** integrated into a static portfolio website hosted on Amazon S3. It uses **HTML, CSS, JavaScript**, and AWS services including **Lambda, API Gateway, and Simple Email Service (SES)**.

---

## 📌 Project Overview

The goal was to create a secure, serverless contact form that emails form submissions directly to my inbox using AWS infrastructure—without relying on third-party services.

---

## 🛠️ Tools & Technologies

- **Frontend:** HTML, CSS, JavaScript
- **Backend:** AWS Lambda (Node.js)
- **API Gateway**: Handles HTTP requests
- **SES (Simple Email Service)**: Sends emails
- **S3 Bucket**: Hosts the static site
- **CloudWatch**: Debugging and error monitoring

---

## ✅ Functional Workflow

1. User fills out the form (Name, Email, Message).
2. JavaScript sends a `POST` request to the API Gateway endpoint.
3. API Gateway triggers a Lambda function.
4. Lambda validates and sends the message to my email using SES.
5. User receives a confirmation or error alert on the site.

---

## 🔧 Setup & Configuration

### 1. **S3 Bucket Setup**
- Created bucket: `latrisha-portfolio-site`
- Enabled static website hosting.
- Uploaded `index.html` and `script.js`.

📸 *Screenshot of S3 bucket:*
![S3 Bucket Contents](screenshots/bucket.png)

---

### 2. **Lambda Function**
- Wrote the logic to parse form data and send an email via SES.
- Configured IAM permissions for SES access.

📸 *Lambda script screenshot:*
![Lambda Code](screenshots/Serverless-Contact-Form-final-project.png)

---

### 3. **API Gateway**
- Created a REST API.
- Set up POST method integration with Lambda.
- Enabled CORS for the frontend domain.

📸 *CloudWatch logs showing initial errors:*
![CloudWatch Error](screenshots/Screenshot-2025-07-22-165532.png)

---

## ⚠️ Common Errors & Debugging

### ❌ Issue: "MessageRejected" (SES error)
- **Cause:** Email not verified in SES sandbox mode.
- **Fix:** Verified both sender and recipient emails in SES console.

📸 *Error in CloudWatch:*
![SES Rejection](screenshots/Contact-Form-Error-2025-07-22-165053.png)

---

### ❌ JavaScript fetch error
- **Cause:** Invalid endpoint or network issue.
- **Fix:** Replaced placeholder endpoint in `script.js` with the correct API Gateway URL.

📸 *JavaScript Error Screenshot:*
![Fetch Error](screenshots/Contact-Form-Test-Error-2.png)

---

### ✅ Success Confirmation
Once the proper SES configuration was in place and the endpoint was updated:

📸 *Success message:*
![Success Confirmation](screenshots/Contact-Form-Test-Success.png)

---

## 📄 JavaScript Snippet (Frontend)

```javascript
form.addEventListener("submit", async (e) => {
  e.preventDefault();
  const formData = new FormData(form);
  const data = {
    name: formData.get("name"),
    email: formData.get("email"),
    message: formData.get("message"),
  };

  try {
    const response = await fetch("https://your-api-id.execute-api.us-east-1.amazonaws.com/prod/contact", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(data),
    });

    if (response.ok) {
      alert("Message sent successfully!");
      form.reset();
    } else {
      alert("Error sending message. Try again.");
    }
  } catch (error) {
    alert("Submission failed. Please check your connection.");
  }
});
📸 Script file:

📂 Git Workflow Documentation (Optional)
If you want to document your GitHub process:

📸 Initializing repo & adding resume.html:

📸 Commit message:

🚀 Live Site
https://latrisha-portfolio-site.s3-website-us-east-1.amazonaws.com

📝 Future Improvements
Integrate CAPTCHA to prevent spam.

Move SES out of sandbox mode for production-level use.

Add client-side form validation.

🙏 Acknowledgments
Thanks to The Knowledge House for guidance and mentorship throughout this project.
