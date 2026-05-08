Role: Expert Frontend Developer & UX Designer for Lean Startups.

Objective: Create a high-conversion, modern Hugo static site for "Unskooling.day," a community-based experiential learning platform in Bangalore. The site must serve as a "smoke test" to validate interest.

Design Philosophy: > * Clean & Playful: Use a "Modern Education" aesthetic (soft rounded corners, high contrast, warm typography like 'Outfit' or 'Quicksand').

Local Trust: Tailor the copy and UI to appeal to parents in gated communities in Bangalore.

Technical Requirements:

Framework: Hugo (using Tailwind CSS for styling).

Data-Driven UI: Structure the layouts so that every section (Mentors, Sessions, Societies) is populated automatically by adding .md files to specific content folders.

Components to Build:

Hero Section: Clear headline "Real-world skills, taught by neighbors, in your community hall." Primary CTA: "Find a Session"; Secondary: "Bring Unskooling to My Society."

The "So What" & Clarity Section: A two-column layout explaining the shift from "rote learning" to "curiosity-led unschooling."

How it Works: A 3-step icon-based horizontal timeline.

Session Directory: A grid view that pulls from content/sessions/*.md. Categories: Music, Swimming, Business.

Mentor Profiles: Cards pulling from content/mentors/*.md, each featuring an "Express Interest" button.

Safety & Quality: A dedicated trust-block highlighting society-vetted mentors.

Gallery: A simple grid for "Previous Classes" to show social proof.

Content Management Logic (Folder Structure):

/content/sessions/: Markdown files with Frontmatter for title, category, price_model, and status (Active/Upcoming).

/content/mentors/: Markdown files with name, skill, bio, and photo.

/content/societies/: Markdown files for specific Bangalore societies to show "Upcoming Sessions in [Society Name]".

Call to Action (CTA) Strategy:

Include a sticky Navigation Bar with a "Sign Up" button.

Place a prominent "Bring Unskooling to My Society" section before the footer specifically for society presidents.

Deliverable: Provide the hugo.toml configuration, a baseof.html template, and the Tailwind-integrated index.html that loops through the content folders.