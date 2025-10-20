# Azure Palm Resort - Luxury Hotel Website

A premium, production-quality, mobile-first static website for Azure Palm Resort, a luxury beachfront hotel in South Florida.

## 🌟 Features

### Core Functionality
- **7 Complete Pages**: Home, Rooms, Amenities, Gallery, Local Attractions, Contact, Legal (Privacy & Terms)
- **Interactive Booking System**: Form validation, localStorage demo storage, mailto fallback
- **Photo Gallery**: Lazy-loaded images, lightbox view, category filtering
- **Contact Forms**: Client-side validation, demo data storage
- **Demo Admin Dashboard**: View bookings and contact messages (accessible at `/demo-admin.html`)
- **Responsive Design**: Mobile-first, optimized for phones, tablets, and desktops

### Performance & SEO
- **Lighthouse-Ready**: Optimized for 90+ performance score
- **Lazy Loading**: Images load on-demand for faster page loads
- **Critical CSS**: Inline hero CSS for instant first paint
- **SEO Optimized**: Schema.org markup, meta tags, OpenGraph/Twitter cards
- **Sitemap & Robots.txt**: Ready for search engine indexing

### Accessibility
- ARIA labels and landmarks
- Keyboard navigation support
- Skip navigation links
- Sufficient color contrast
- Alt text for all images

## 📁 Project Structure

```
/
├── index.html                  # Homepage
├── rooms.html                  # Room listings
├── amenities.html              # Amenities & About
├── gallery.html                # Photo gallery
├── attractions.html            # Local area attractions
├── contact.html                # Contact form
├── privacy.html                # Privacy policy
├── terms.html                  # Terms & conditions
├── demo-admin.html             # Demo admin dashboard
├── sitemap.xml                 # SEO sitemap
├── robots.txt                  # Search engine directives
├── assets/
│   ├── css/
│   │   ├── styles.css          # Main stylesheet
│   │   ├── rooms.css           # Rooms page styles
│   │   ├── gallery.css         # Gallery styles
│   │   ├── amenities.css       # Amenities styles
│   │   ├── attractions.css     # Attractions styles
│   │   ├── contact.css         # Contact styles
│   │   ├── admin.css           # Admin dashboard styles
│   │   └── legal.css           # Legal pages styles
│   ├── js/
│   │   ├── main.js             # Core JavaScript
│   │   ├── booking.js          # Booking system
│   │   ├── gallery.js          # Gallery functionality
│   │   ├── contact.js          # Contact form
│   │   └── admin.js            # Admin dashboard
│   └── images/                 # Image assets
└── README.md                   # This file
```

## 🚀 Deployment on Replit

### Quick Start

1. **Your site is ready!** All files are in place and configured.

2. **Test Locally**: Open `index.html` in a browser to view the site.

3. **Replit Static Deployment**:
   - Click the **"Deploy"** button in Replit
   - Select **"Static"** deployment type
   - Your site will be live at `https://your-repl-name.repl.co`

### Custom Domain Setup (Optional)

1. In Replit, go to your deployment settings
2. Click "Add Custom Domain"
3. Follow DNS configuration instructions
4. Update all URLs in the HTML files from `azurepalmresort.com` to your domain

## 📊 Demo Admin Dashboard

Access the demo admin panel at: `/demo-admin.html`

**Features:**
- View all booking requests
- View all contact messages
- See booking statistics and estimated revenue
- Clear demo data

**Note:** This is a demonstration only. Data is stored in browser localStorage and is NOT secure for production use.

## 🧪 Testing

### Lighthouse Testing

1. Open your deployed site in Chrome
2. Open Developer Tools (F12)
3. Go to "Lighthouse" tab
4. Select "Mobile" device
5. Check "Performance", "Accessibility", "SEO", "Best Practices"
6. Click "Generate report"
7. Target: Performance ≥ 90

### Browser Testing

Test on multiple devices and browsers:
- **Mobile**: iPhone (Safari), Android (Chrome)
- **Tablet**: iPad (Safari), Android tablet (Chrome)
- **Desktop**: Chrome, Firefox, Safari, Edge

### Functionality Testing

- ✅ All navigation links work
- ✅ Booking modal opens and validates input
- ✅ Gallery lightbox displays images
- ✅ Contact form validates and submits
- ✅ Mobile menu toggles correctly
- ✅ All buttons and CTAs function
- ✅ Admin dashboard displays bookings

## 🔄 Converting to Production Backend

### Step 1: Choose Your Backend Stack

**Option A: Node.js + Express**
```javascript
// Example backend structure
/backend
  /routes
    bookings.js
    contacts.js
  /models
    Booking.js
    Contact.js
  /controllers
  server.js
```

**Option B: Python + Flask/Django**
```python
# Example Flask structure
/backend
  app.py
  models.py
  routes.py
  config.py
```

### Step 2: Database Setup

**Recommended: PostgreSQL**

```sql
-- Bookings Table
CREATE TABLE bookings (
    id SERIAL PRIMARY KEY,
    guest_name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(50) NOT NULL,
    room_type VARCHAR(100) NOT NULL,
    check_in DATE NOT NULL,
    check_out DATE NOT NULL,
    special_requests TEXT,
    status VARCHAR(50) DEFAULT 'pending',
    total_amount DECIMAL(10,2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Contacts Table
CREATE TABLE contacts (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(50) NOT NULL,
    message TEXT NOT NULL,
    status VARCHAR(50) DEFAULT 'new',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Step 3: Payment Integration

**Stripe Integration Example:**

```javascript
const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY);

app.post('/api/create-payment-intent', async (req, res) => {
    const { amount } = req.body;
    
    const paymentIntent = await stripe.paymentIntents.create({
        amount: amount * 100, // Convert to cents
        currency: 'usd',
        metadata: { booking_id: req.body.bookingId }
    });
    
    res.json({ clientSecret: paymentIntent.client_secret });
});
```

### Step 4: Email Notifications

**Example with SendGrid:**

```javascript
const sgMail = require('@sendgrid/mail');
sgMail.setApiKey(process.env.SENDGRID_API_KEY);

async function sendBookingConfirmation(booking) {
    const msg = {
        to: booking.email,
        from: 'reservations@azurepalmresort.com',
        subject: 'Booking Confirmation - Azure Palm Resort',
        html: `<strong>Thank you for your booking!</strong>...`
    };
    
    await sgMail.send(msg);
}
```

### Step 5: Update Frontend

Replace localStorage calls with API calls:

```javascript
// Before (Demo):
localStorage.setItem('bookings', JSON.stringify(booking));

// After (Production):
const response = await fetch('/api/bookings', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(booking)
});
const result = await response.json();
```

## 🛡️ Security Recommendations for Production

1. **HTTPS Only**: Ensure SSL certificate is active
2. **Input Validation**: Server-side validation for all forms
3. **SQL Injection Prevention**: Use parameterized queries
4. **XSS Protection**: Sanitize all user inputs
5. **CSRF Tokens**: Implement for form submissions
6. **Rate Limiting**: Prevent spam and abuse
7. **Environment Variables**: Store API keys securely
8. **Authentication**: Secure admin dashboard with proper auth
9. **PCI Compliance**: If handling payments directly
10. **GDPR/Privacy Compliance**: Follow data protection regulations

## 🎨 Customization

### Brand Colors

Edit in `assets/css/styles.css`:

```css
:root {
    --primary-color: #0891b2;      /* Main brand color */
    --accent-gold: #f59e0b;        /* CTA buttons */
    --text-dark: #1f2937;          /* Primary text */
}
```

### Hotel Information

Update contact details throughout HTML files:
- Phone: `+1 (305) 555-0100`
- Email: `reservations@azurepalmresort.com`
- Address: `1234 Ocean Boulevard, Miami Beach, FL 33139`

### Room Prices

Edit in `assets/js/booking.js`:

```javascript
const prices = {
    'Standard Ocean View': 299,
    'Deluxe Suite': 499,
    'Presidential Suite': 899
};
```

## 📦 Download Site Files

To download all files as a zip:

```bash
# In terminal/command line
zip -r azure-palm-resort.zip . -x "*.git*" -x "node_modules/*"
```

Or use Replit's built-in "Download as zip" option from the file menu.

## 📞 Support & Documentation

- **Demo Site**: Built by Kanik Web Studio
- **Framework**: Vanilla HTML/CSS/JavaScript
- **Icons**: Font Awesome 6.4.0
- **Fonts**: Google Fonts (Playfair Display, Poppins)

## 📝 License

This is a demonstration project. For production use, ensure you have appropriate licenses for all assets and comply with relevant laws and regulations.

## 🚀 Next Steps

1. ✅ Deploy to Replit Static Hosting
2. ✅ Test on multiple devices
3. ✅ Run Lighthouse audit
4. ⏭️ Replace placeholder images with real photos
5. ⏭️ Update hotel information and content
6. ⏭️ Add backend for real booking functionality
7. ⏭️ Integrate payment gateway (Stripe recommended)
8. ⏭️ Set up email notifications
9. ⏭️ Add calendar for real-time availability
10. ⏭️ Secure admin dashboard with authentication

---

**Built with ❤️ for Azure Palm Resort**

*This is a demo/template. Always consult with legal and technical professionals before deploying to production.*
