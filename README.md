# **How to Integrate ConvertBox Events with Your Custom JavaScript for Advanced Tracking**

---

### **Introduction: Make Every Click Count**

You’ve spent hours designing a stunning ConvertBox form. It's capturing leads—but what’s next?

What if you could track what happens *after* someone sees or submits your ConvertBox? What if you could send that data to Google Analytics, fire a Facebook Pixel event, or even pass it directly to your CRM?

Well, you can. And in this article, I’ll show you **exactly how to integrate ConvertBox events with your custom JavaScript** for advanced tracking. No fluff—just practical steps, easy code, and real-life examples.

---

### **What Is ConvertBox and Why It’s a Game Changer**

ConvertBox is a powerful lead generation tool that helps you show popups, forms, and surveys to website visitors.

But here’s the truth…

Most users don’t take full advantage of ConvertBox. They only use the built-in forms and collect leads. That’s good, but not *great*.

If you want to:

* Track leads in Google Analytics or Facebook
* Send captured data to your CRM
* Trigger custom scripts when a form is submitted

…then you need to tap into **ConvertBox’s event system** and integrate it with **custom JavaScript**.

It might sound technical—but don’t worry. You’ll get the hang of it even if you're not a developer.

---

### **What Are ConvertBox Event Hooks?**

ConvertBox provides something called “event hooks.” These are **JavaScript callbacks** that get fired when certain actions happen on the ConvertBox, like:

* `onShow` – when the ConvertBox appears
* `onClose` – when a user closes it
* `onSubmit` – when a user submits the form

These events allow you to “listen” and then take action.

Let’s say you want to fire a Facebook Pixel event every time someone submits a form. You can use the `onSubmit` hook and add your custom JavaScript to do that. It’s as powerful as it is simple.

---

### **Where to Add Your Custom Code in ConvertBox**

Before writing any code, let’s first find where to put it inside ConvertBox.

**Step-by-step:**

1. Login to your ConvertBox dashboard
2. Open the form or popup you want to edit
3. Go to **Settings > Advanced > Custom Scripts**
4. Paste your JavaScript inside the field that says `Custom JavaScript`

This code will only run when that ConvertBox is shown on your website.

**Important Tip:** Make sure the ConvertBox embed code is already installed on your site before testing your script.

---

### **Example: Track Form Submissions with Google Tag Manager**

Here’s a practical example using Google Tag Manager (GTM):

```javascript
window.ConvertBox = window.ConvertBox || [];
window.ConvertBox.push(function(cb) {
    cb.onSubmit(function(data) {
        console.log("Form submitted!", data);
        dataLayer.push({
            event: 'convertbox_form_submit',
            formData: data
        });
    });
});
```

Here’s what this code does:

* Waits for ConvertBox to load
* Listens for the form `onSubmit` event
* Pushes an event called `convertbox_form_submit` to GTM’s dataLayer
* Passes the form data (like name, email) too

Once it’s in GTM, you can use it to trigger conversions, send data to Google Analytics 4, or anything else.

---

### **Use Case: Fire Facebook Pixel Events on Submit**

Want to track form submits as Facebook conversions?

Add this code in your ConvertBox:

```javascript
window.ConvertBox = window.ConvertBox || [];
window.ConvertBox.push(function(cb) {
    cb.onSubmit(function(data) {
        fbq('track', 'Lead', {
            content_name: 'ConvertBox Lead Form'
        });
    });
});
```

You’ll see “Lead” conversions show up in your Facebook Ads Manager!

This helps you measure ad performance more accurately and retarget visitors who didn’t complete the funnel.

---

### **Send Form Data to Your CRM or Backend**

Here’s how to send ConvertBox form data to your server or CRM using JavaScript’s `fetch()` API:

```javascript
window.ConvertBox = window.ConvertBox || [];
window.ConvertBox.push(function(cb) {
    cb.onSubmit(function(data) {
        fetch('https://yourdomain.com/api/lead', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        });
    });
});
```

This sends the form data (like name, email) to your server for storage or further automation. Just replace the URL with your own CRM or webhook endpoint.

---

### **Common Issues & Fixes**

Let’s be honest—JavaScript can sometimes break. Here are common problems and how to fix them:

* ❌ **Problem:** Nothing happens when the form is submitted
  ✅ **Fix:** Check if your code is wrapped inside `window.ConvertBox.push()`

* ❌ **Problem:** JS error in browser
  ✅ **Fix:** Open Chrome DevTools > Console tab to debug

* ❌ **Problem:** GTM event doesn’t fire
  ✅ **Fix:** Make sure GTM’s dataLayer is initialized **before** ConvertBox loads

* ❌ **Problem:** Events firing twice
  ✅ **Fix:** Double-check that you're not triggering the same function multiple times (use flags or remove duplicate code)

---

### **Best Practices for Clean Integration**

Here are some simple yet powerful tips to avoid future issues:

* ✅ Always use `window.ConvertBox.push()` to wrap your code
* ✅ Load ConvertBox *after* your page fully loads (put script at the bottom)
* ✅ Avoid using jQuery or third-party libraries that may conflict
* ✅ Use `console.log()` while testing, then remove it on production
* ✅ Clearly name your events for analytics (e.g., `convertbox_form_submit`, not `event1`)

---

### **Final Thoughts: Tracking = Growth**

If you don’t track, you’re flying blind.

By integrating ConvertBox events with your custom JavaScript, you unlock **the power of data**. You’ll understand:

* Which ConvertBoxes convert best
* Where your leads are coming from
* How your marketing campaigns are performing

It’s not about being a tech wizard. It’s about being a smart marketer.

**So take this guide, test it out, and start capturing better insights today.**

---

### **FAQs**

**Q. Can I integrate ConvertBox with Google Analytics 4?**
**A.** Yes. Use the `onSubmit` hook to push events to GTM, which then sends data to GA4.

**Q. Is it safe to use JavaScript in ConvertBox?**
**A.** Yes, as long as the code is clean and you test it before going live.

**Q. Can I track clicks on buttons inside ConvertBox?**
**A.** Yes, but you’ll need to assign `onClick` events using custom HTML blocks.

**Q. Can I use ConvertBox with Zapier?**
**A.** ConvertBox doesn’t have direct Zapier integration yet, but you can use webhooks.
