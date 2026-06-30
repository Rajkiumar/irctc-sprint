## Problem 1: Tatkal Booking Crashes at 10:00 AM

### What is broken

During Tatkal booking hours, users frequently experience slow loading, session timeouts, booking failures, and unexplained errors when demand spikes. The platform provides little feedback about queue position, system load, or likelihood of successful booking.

### Affected users

Passengers attempting Tatkal bookings, particularly commuters, emergency travelers, students, and business travelers who depend on last-minute reservations.

### Frequency

Daily during Tatkal opening hours, especially around 10:00 AM for AC classes and 11:00 AM for non-AC classes.

### Current flow — step by step

1. User opens IRCTC around 9:50 AM.
2. User logs into their account.
3. User searches for a train and selects the Tatkal quota.
4. User keeps the booking page ready before quota opening.
5. At quota opening time, the user refreshes and attempts booking.
6. Passenger details and preferences are entered.
7. User clicks Continue or Proceed to payment.
8. The system becomes slow, freezes, times out, or displays an error.
9. User retries multiple times.
10. By the time the page responds, available Tatkal seats are exhausted.

### Where exactly it breaks

Step 8. The transition from booking confirmation to payment frequently fails under peak load. The user receives insufficient feedback regarding whether the request is being processed, queued, or rejected.

## Problem 2: Login Session Error Page Provides No Recovery Guidance [Self-Discovered]

### How I found it

While attempting to access IRCTC services through the web portal, I navigated between pages and was redirected to an error screen instead of the expected login flow.

### Screenshot: assets/screenshots/login-session-error.png

### What is broken

When a session expires or the user performs an action such as refresh, back navigation, opening a new tab, or remaining inactive, IRCTC redirects to a generic error page displaying "Sorry!!! Please Try again!!"

The page lists multiple possible causes but does not identify the actual cause of the failure. Users receive no clear recovery path other than manually restarting the login process.

Affected users
Returning users with expired sessions
Users navigating with browser controls
Users researching trains in multiple tabs
Elderly and less tech-savvy users
Frequency

Common. Likely occurs thousands of times daily due to normal browsing behavior, session timeouts, and multi-tab usage.

Current flow — step by step
User opens IRCTC website.
User begins searching for trains or account services.
User spends time comparing trains or checking availability.
User refreshes the page, uses the browser back button, or leaves the tab idle.
Session becomes invalid or expires.
User attempts another action.
System redirects to /nget/error.
Generic error page appears.
User cannot determine the exact issue.
User restarts the process from the beginning.
Where exactly it breaks

Step 7.

Instead of detecting the specific error condition and guiding the user appropriately, the system displays a generic failure page containing multiple possible reasons. The user is not informed which action triggered the error or how to recover without losing progress.

### Severity

High.

The issue interrupts active booking journeys, increases abandonment rates, and forces users to repeat previously completed actions.

## Problem 3: E-Wallet User Guide Documentation Fails to Load [Self-Discovered]

### How I found it

While exploring account and payment-related resources on IRCTC, I attempted to open the E-Wallet User Guide PDF provided by the platform.

### Screenshot

Screenshot: assets/screenshots/ewallet-guide-blank-page.png

What is broken

The E-Wallet User Guide link opens a blank browser page instead of displaying the PDF document.

The system provides no indication whether:

the file is missing,
the server failed,
the PDF is loading,
browser support is unavailable,
or the document has been removed.

Users are left with an empty screen and no guidance.

Affected users
New users trying to understand IRCTC E-Wallet
Users setting up digital payment methods
First-time travelers unfamiliar with IRCTC wallet features
Elderly users requiring documentation support
Frequency

Occurs every time the broken document link is accessed.

Current flow — step by step
User visits IRCTC website.
User navigates to payment or E-Wallet information.
User notices a link to the E-Wallet User Guide.
User clicks the guide link.
Browser opens a new tab.
URL points to an expected PDF document.
Page loads but remains blank.
User waits for content to appear.
No document is displayed.
User abandons the help resource.
Where exactly it breaks

Step 7.

The PDF resource fails to render correctly and the system does not provide any fallback behavior such as:

download option,
error notification,
retry mechanism,
alternate documentation page.

### Severity

Medium.

Although it does not directly block ticket booking, it prevents users from accessing official guidance for a payment feature and reduces trust in the platform's help resources.