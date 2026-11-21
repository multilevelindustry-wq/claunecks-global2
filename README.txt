CLAUNECKS GLOBAL (claunecks.com) — FIREBASE-READY WEBSITE STARTER
===========================================

WHAT'S INCLUDED
- Redesigned, responsive Claunecks Global home page and shared navigation/footer.
- Eight connected marketplace sections: Skills, Items, Artwork, Books/Media/Downloads, Community, Apps, Property and Jobs.
- 30 category pages each for Skills, Items, Artwork and Jobs; 42 Downloads; 36 Community; 26 Apps; 36 Property pages.
- Firebase Authentication email/password registration and login.
- Firestore profile/listing records and Firebase Storage multi-image upload.
- Listing search/filter, individual seller storefront pages, saved listings, user dashboard, likes and threaded-per-listing comments collection.
- WhatsApp enquiry button for digital items, with item title, reference, category, section, location, price and referring page included in the prefilled message.
- 20 admin workspace pages with Firebase-authenticated admin gate.
- SEO page generator in Admin > SEO sitemap generator. It generates one title-based .html file per published listing plus sitemap.xml and a directory index, bundled in a ZIP.
- AdSense publisher meta tag and loader included in every authored HTML page, including generated SEO pages.
- Firestore and Storage security rules included.

FIREBASE SETUP
1. Open Firebase Console for project neostore-81b57.
2. Enable Authentication > Email/Password.
3. Create a Cloud Firestore database.
4. Enable Firebase Storage.
5. Publish firebase/firestore.rules and firebase/storage.rules (or deploy with Firebase CLI using firebase.json).
6. Host this folder on HTTPS (Firebase Hosting, GitHub Pages with suitable backend, or another static host).
7. The Firebase web config is in js/firebase-config.js. Firebase web config/API key is not a server secret; security must come from Authentication, Firestore rules, Storage rules and authorized domains.

ADMIN AUTHORIZATION
- Create an admin user through Firebase Authentication (email/password).
- Copy that user's Firebase Authentication UID.
- In Firestore, create collection `admins`, document ID exactly equal to that UID, with fields: { "active": true, "role": "admin" }.
- The admin login checks this record. Do not use a shared password embedded in HTML/JS. The previous requested browser password is intentionally not embedded because it would be visible to every visitor.
- Add stricter custom claims / server-side admin management before production. Firestore rules prevent client-side creation of admin records.

WHATSAPP DIGITAL ITEM ENQUIRIES
- In a listing form, enter the uploader's WhatsApp number in international digits without + or spaces (example: 2348012345678), or add a wa.me URL.
- Get item on WhatsApp opens a prefilled message with listing title, reference, category, section, country/city, price and the referring page. User can edit/send the message.
- This section has NO Paystack or PayPal checkout in this version, per the latest instruction. Do not put private download file URLs in public listings.

SEO GENERATOR NOTES
- Sign in as admin, open Admin > SEO sitemap generator, enter your real domain, choose target length and generate.
- The ZIP contains individual title-slug-id.html files, a listings-listings-index.html directory page and sitemap.xml.
- The requested 2,000-word target is generated from the listing title, description and structured contextual sections. Review generated pages for accuracy and uniqueness before publishing. Do not publish repetitive or thin pages at scale: Google may ignore or penalize scaled content created primarily to manipulate search rankings. Only publish pages with useful, truthful, original information. No generator can guarantee indexing, ranking or virality.
- Upload the generated HTML files to your domain root (or update sitemap URLs if using a subfolder), then submit sitemap.xml in Google Search Console. Configure the canonical domain in the generator. Keep a copy of your sitemap.
- Existing category pages are navigation pages. User-uploaded listing pages are generated from Firestore when the admin runs the generator; the browser does not automatically upload them to hosting.

ADSENSE
- Publisher script and google-adsense-account meta are added to every HTML page. Ad placement and approval are controlled by Google. Add ad units only where appropriate and comply with AdSense policies.
- AdSense must never be used for incentivized views/clicks. This build deliberately does not force users to watch or click three AdSense ads to unlock app downloads. Normal, policy-compliant ad placements are used instead.

IMPORTANT PRODUCTION WORK
This is a Firebase-connected starter, not a fully audited marketplace. Before launch add: email verification enforcement, phone verification if required, Cloud Functions for trusted counters/notifications, robust search indexing, image moderation, abuse/rate limits, reports and blocking, privacy/terms/copyright workflows, backups, secure upload quotas, country/currency locale formatting, and admin audit logs. Firestore indexes may be requested by Firebase when compound queries are first used; create them from the console link in the error.

SECURITY
Never collect bank/card details in plain text. Payout processing and payment integrations require a secure server and access-controlled workflows. This build does not implement payment checkout for digital items.


FIXES IN THIS UPDATE — VIEWS AND IMAGE UPLOAD URLS
- Every successful load of a public listing detail page adds exactly one view, including repeat visits by the same visitor. It is not deduplicated by user or browser.
- Public Firestore rules now permit only a one-step increment of the views field without requiring visitors to sign in.
- All eight upload forms now show uploaded image previews and the Firebase download URL(s) after upload. The URLs are stored in the listing as images, imageUrls, and the primary imageUrl.
- After uploading this update, publish the included Firebase rules to your Firebase project (Firebase Console > Firestore Database > Rules, and Storage > Rules), or run: firebase deploy --only firestore:rules,storage.
