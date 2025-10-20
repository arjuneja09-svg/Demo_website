# Azure Palm Resort - Luxury Hotel Website

## Overview

Azure Palm Resort is a luxury beachfront hotel demo website built as a showcase project for Kanik Web Studio. This is a fully functional, production-quality static website featuring a complete hotel booking experience, photo gallery, amenities showcase, and contact system. The project demonstrates modern web development best practices including mobile-first design, performance optimization, accessibility, and SEO.

**Status:** ✅ Complete and ready for deployment

**Key Features:**
- 7 complete pages (Home, Rooms, Amenities, Gallery, Attractions, Contact, Legal)
- Interactive booking and contact forms with client-side validation
- Demo admin dashboard for viewing submissions at `/demo-admin.html`
- Responsive image gallery with lightbox and filtering
- localStorage-based demo data persistence
- Fully responsive, mobile-first design (phone, tablet, desktop, laptop)
- SEO optimized with schema markup and meta tags
- Sales materials included for marketing purposes

## User Preferences

Preferred communication style: Simple, everyday language.

## Recent Updates (October 19, 2025)

**Complete Website Build:**
- Built all 7 main pages with luxury coastal design
- Implemented booking system with form validation and mailto fallback
- Created photo gallery with lazy loading and lightbox functionality
- Added demo admin dashboard to view bookings and contact messages
- Implemented SEO optimization (meta tags, schema.org, sitemap, robots.txt)
- Created comprehensive README with deployment and backend migration guide
- Generated sales materials (5 headlines, 3 email templates, sales sheet)
- Configured Replit static deployment workflow
- Website is live and accessible on port 5000

## System Architecture

### Frontend Architecture

**Technology Stack:**
- Pure HTML5, CSS3, and vanilla JavaScript (no frameworks)
- Custom CSS with CSS variables for theming
- Google Fonts (Playfair Display for headings, Poppins for body text)
- Font Awesome 6.4.0 for icons

**Design Pattern:**
- Mobile-first responsive design
- Component-based CSS organization (separate stylesheets per page)
- Critical CSS inlined in homepage for performance
- CSS custom properties for consistent theming across all pages

**Page Structure:**
- Shared navigation and footer across all pages
- Modular JavaScript files per feature (booking.js, contact.js, gallery.js, admin.js)
- Main.js handles global functionality (navigation, scroll effects)

### Data Storage

**Client-Side Storage Strategy:**
- localStorage used exclusively for demo purposes
- Two main data stores:
  - `azurePalmBookings`: Array of booking objects
  - `azurePalmContacts`: Array of contact form submissions

**Data Models:**

Booking Object:
```javascript
{
  id: string,           // Unique booking ID
  name: string,
  email: string,
  phone: string,
  roomType: string,     // "Standard" | "Deluxe" | "Presidential"
  checkIn: string,      // ISO date
  checkOut: string,     // ISO date
  guests: number,
  specialRequests: string,
  status: string,       // "Pending" | "Confirmed" | "Cancelled"
  bookingDate: string   // ISO timestamp
}
```

Contact Object:
```javascript
{
  id: string,
  name: string,
  email: string,
  phone: string,
  subject: string,
  message: string,
  submittedAt: string   // ISO timestamp
}
```

### Form Handling & Validation

**Booking System:**
- Client-side validation for all form fields
- Email and phone format validation using regex
- Date validation (check-in must be before check-out)
- Data saved to localStorage
- Mailto fallback for email notifications
- Success modal with booking summary
- Print and PDF download functionality (client-side generated)

**Contact Forms:**
- Similar validation pattern to booking system
- Separate localStorage storage for contact messages
- Mailto fallback for notifications
- Success confirmation modal

### Performance Optimizations

**Image Strategy:**
- Lazy loading implemented for gallery images
- WebP format recommended (currently using placeholder URLs)
- Responsive images with aspect-ratio CSS for layout stability

**CSS Optimization:**
- Critical CSS inlined for above-the-fold content (hero section)
- Page-specific CSS loaded separately to reduce initial load
- CSS minification recommended for production

**JavaScript:**
- Modular approach with separate files per feature
- No dependencies or frameworks (minimal bundle size)
- Async/defer loading where appropriate

### Accessibility Features

- ARIA labels on interactive elements
- Skip navigation link for keyboard users
- Semantic HTML5 structure
- Sufficient color contrast ratios
- Alt text on all images
- Keyboard navigation support
- Focus state styling

### SEO Implementation

**Meta Tags:**
- Page-specific title and description tags
- OpenGraph tags for social sharing
- Twitter card markup
- Canonical URLs for all pages

**Structured Data:**
- Schema.org Hotel JSON-LD markup (ready to implement)
- Sitemap.xml for search engines
- Robots.txt with crawl directives

**URL Structure:**
- Clean, semantic URLs (e.g., /rooms.html, /amenities.html)
- Descriptive page names

### Demo Admin Dashboard

**Purpose:**
- Demonstrates how booking/contact data would appear in a real system
- Accessible at `/demo-admin.html` (no authentication - demo only)
- Read-only view of localStorage data

**Features:**
- Statistics cards (total bookings, contacts, revenue calculations)
- Tabular display of bookings with calculated totals
- Contact messages listing
- Clear messaging that this is demo-only (not production-ready)

**Security Considerations:**
- Explicitly marked as not for production use
- Warning messages about localStorage limitations
- No sensitive data should be stored in this demo

### Navigation System

**Responsive Navigation:**
- Desktop: Horizontal menu bar with hover states
- Mobile: Hamburger menu with slide-out drawer
- Sticky navigation with scroll-based transparency
- Active page highlighting
- Book Now CTA button in navigation

**Scroll Behavior:**
- Smooth scroll enabled
- Navbar transparency changes at 100px scroll
- Mobile menu auto-closes on link click

## External Dependencies

### CDN Resources

**Google Fonts:**
- Playfair Display (weights: 400, 600, 700)
- Poppins (weights: 300, 400, 500, 600)
- Loaded with display=swap for performance

**Font Awesome:**
- Version 6.4.0 from cdnjs.cloudflare.com
- Used for icons throughout the site (navigation, amenities, social media)

### Email Integration

**Mailto Fallback:**
- All form submissions generate mailto: links
- Booking form creates pre-filled email to hotel address
- Contact form creates pre-filled inquiry email
- Serves as zero-cost demo solution without backend

### Maps Integration

**Google Maps:**
- Embedded iframe on Local Attractions page
- Placeholder for hotel location
- Can be replaced with Google Maps API for enhanced functionality

### Browser APIs

**localStorage:**
- Primary data persistence mechanism for demo
- Stores booking and contact form submissions
- No expiration or size limits enforced

**Print API:**
- Window.print() for booking confirmations
- CSS media queries for print-friendly layouts

### Future Integration Points

**Payment Processing:**
- Currently not implemented (demo only)
- Ready for Stripe/PayPal integration
- Booking form structure supports payment gateway addition

**Backend Database:**
- localStorage serves as temporary substitute
- Structure supports easy migration to REST API
- Data models ready for database schema implementation

**Email Service:**
- Currently using mailto: links
- Ready for SendGrid/Mailgun integration
- Form validation already in place

**Real-time Availability:**
- Static room availability shown
- Structure supports calendar API integration
- Date picker ready for availability checking