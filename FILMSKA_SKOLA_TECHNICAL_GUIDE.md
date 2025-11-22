# FILMSKA ŠKOLA - Technical Implementation Guide

## QUICK START INSTRUCTIONS FOR CLAUDE

When generating code for this website, follow these steps:

### 1. INITIAL SETUP
```bash
# Project structure
src/
  components/
    FilmSchoolWebsite.jsx  # Main component
  assets/
    # Placeholder for images
```

### 2. REQUIRED IMPORTS
```jsx
import React, { useState, useEffect, useRef } from 'react';
import { 
  Camera, Film, Play, Check, X, 
  MapPin, Mail, Phone, Instagram,
  Clock, Calendar, Users, Award,
  ChevronDown, Menu, Loader
} from 'lucide-react';
```

### 3. COLOR SYSTEM
```javascript
const colors = {
  background: {
    primary: '#0a0a0a',
    secondary: '#1a1a1a',
    card: '#1e1e1e',
  },
  accent: {
    gold: '#FFB800',
    goldLight: '#D4AF37',
    red: '#8B0000',
    redLight: '#A52A2A',
  },
  text: {
    primary: '#FFFFFF',
    secondary: '#F5F5F5',
    muted: '#A0A0A0',
  }
};
```

### 4. COMPONENT STRUCTURE

```jsx
const FilmSchoolWebsite = () => {
  // State management
  const [activeWeek, setActiveWeek] = useState(null);
  const [activeFaq, setActiveFaq] = useState(null);
  const [enrolledCount, setEnrolledCount] = useState(3); // 3 spots taken
  const [formData, setFormData] = useState({});
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [isVideoPlaying, setIsVideoPlaying] = useState(false);

  // Refs for scroll animations
  const heroRef = useRef(null);
  const videoRef = useRef(null);

  // Scroll effects
  useEffect(() => {
    const handleScroll = () => {
      // Parallax and fade effects
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  return (
    <div className="bg-[#0a0a0a] text-white">
      {/* Navigation */}
      <Navigation />
      
      {/* Hero Section */}
      <HeroSection />
      
      {/* Video Trailer */}
      <VideoSection />
      
      {/* Concept Description */}
      <ConceptSection />
      
      {/* Target Audience */}
      <AudienceSection />
      
      {/* How It Works */}
      <HowItWorksSection />
      
      {/* Curriculum */}
      <CurriculumSection />
      
      {/* Pricing */}
      <PricingSection />
      
      {/* Location */}
      <LocationSection />
      
      {/* Instructor */}
      <InstructorSection />
      
      {/* Gallery */}
      <GallerySection />
      
      {/* Enrollment Slots */}
      <EnrollmentSlotsSection />
      
      {/* Application Form */}
      <ApplicationFormSection />
      
      {/* FAQ */}
      <FAQSection />
      
      {/* Contact/Footer */}
      <FooterSection />
    </div>
  );
};
```

### 5. SECTION TEMPLATES

#### Hero Section Template
```jsx
const HeroSection = () => (
  <section className="relative min-h-screen flex items-center justify-center overflow-hidden">
    {/* Background with overlay */}
    <div className="absolute inset-0 z-0">
      <div className="absolute inset-0 bg-gradient-to-b from-black/70 via-black/50 to-black z-10" />
      {/* Background image placeholder */}
      <div className="w-full h-full bg-[#1a1a1a]" />
    </div>
    
    {/* Content */}
    <div className="relative z-20 container mx-auto px-4 text-center">
      <h1 className="text-5xl md:text-7xl font-bold mb-6 animate-fade-in">
        🎥 7 Veličanstvenih
      </h1>
      <p className="text-xl md:text-2xl mb-4 text-[#D4AF37]">
        Filmska avantura za 7 odabranih
      </p>
      <p className="text-lg md:text-xl mb-8 max-w-3xl mx-auto">
        Filmska škola za radoznale, hrabre i kreativne.<br />
        7 nedelja. 7 žanrova. 7 uloga. 7 polaznika.<br />
        Jedna filmska ekipa.
      </p>
      <div className="flex gap-4 justify-center">
        <button className="bg-[#8B0000] hover:bg-[#A52A2A] px-8 py-4 rounded-lg text-lg font-semibold transition-all transform hover:scale-105">
          👉 Prijavi se
        </button>
        <button className="border-2 border-[#FFB800] text-[#FFB800] hover:bg-[#FFB800] hover:text-black px-8 py-4 rounded-lg text-lg font-semibold transition-all">
          👉 Pogledaj trejler
        </button>
      </div>
    </div>
  </section>
);
```

#### Pricing Card Template
```jsx
const PricingCard = ({ title, option, payments, recommended }) => (
  <div className={`relative p-8 rounded-lg border-2 ${
    recommended 
      ? 'border-[#FFB800] bg-[#1a1a1a]' 
      : 'border-[#333] bg-[#1e1e1e]'
  }`}>
    {recommended && (
      <div className="absolute -top-4 left-1/2 transform -translate-x-1/2 bg-[#FFB800] text-black px-4 py-1 rounded-full text-sm font-semibold">
        Najpopularnije
      </div>
    )}
    <h3 className="text-2xl font-bold mb-4">{title}</h3>
    <div className="space-y-3">
      {payments.map((payment, idx) => (
        <div key={idx} className="flex items-start gap-3">
          <Check className="w-5 h-5 text-[#FFB800] flex-shrink-0 mt-1" />
          <span>{payment}</span>
        </div>
      ))}
    </div>
  </div>
);
```

#### Curriculum Week Accordion Template
```jsx
const WeekAccordion = ({ number, title, topics, isActive, onClick }) => (
  <div className="border-b border-[#333]">
    <button
      onClick={onClick}
      className="w-full p-6 flex items-center justify-between hover:bg-[#1a1a1a] transition-colors"
    >
      <div className="flex items-center gap-4">
        <div className="w-12 h-12 rounded-full bg-[#FFB800] text-black font-bold flex items-center justify-center text-xl">
          {number}
        </div>
        <h3 className="text-xl font-bold">{title}</h3>
      </div>
      <ChevronDown className={`w-6 h-6 transition-transform ${
        isActive ? 'rotate-180' : ''
      }`} />
    </button>
    {isActive && (
      <div className="px-6 pb-6 space-y-2">
        {topics.map((topic, idx) => (
          <div key={idx} className="flex items-start gap-2">
            <Film className="w-4 h-4 text-[#FFB800] flex-shrink-0 mt-1" />
            <span className="text-[#F5F5F5]">{topic}</span>
          </div>
        ))}
      </div>
    )}
  </div>
);
```

#### Enrollment Slots Visual Template
```jsx
const EnrollmentSlots = ({ enrolled = 3, total = 7 }) => (
  <div className="bg-[#1a1a1a] p-8 rounded-lg">
    <h3 className="text-2xl font-bold mb-6 text-center">
      Preostala mesta
    </h3>
    <div className="flex justify-center gap-3 mb-6">
      {Array.from({ length: total }).map((_, idx) => (
        <div
          key={idx}
          className={`w-16 h-16 rounded-full flex items-center justify-center text-xl font-bold border-2 transition-all ${
            idx < enrolled
              ? 'bg-[#FFB800] border-[#FFB800] text-black'
              : 'bg-transparent border-[#333] text-[#666]'
          }`}
        >
          {idx < enrolled ? '✓' : idx + 1}
        </div>
      ))}
    </div>
    <p className="text-center text-lg">
      Kurs počinje kada se popuni svih 7 mesta.
    </p>
    <p className="text-center text-[#FFB800] font-semibold mt-2">
      {total - enrolled} mesta preostalo!
    </p>
  </div>
);
```

#### Form Input Template
```jsx
const FormInput = ({ label, type = "text", required, ...props }) => (
  <div className="mb-4">
    <label className="block text-sm font-semibold mb-2">
      {label} {required && <span className="text-[#8B0000]">*</span>}
    </label>
    <input
      type={type}
      required={required}
      className="w-full bg-[#1a1a1a] border border-[#333] rounded-lg px-4 py-3 focus:outline-none focus:border-[#FFB800] transition-colors"
      {...props}
    />
  </div>
);

const FormTextarea = ({ label, required, ...props }) => (
  <div className="mb-4">
    <label className="block text-sm font-semibold mb-2">
      {label} {required && <span className="text-[#8B0000]">*</span>}
    </label>
    <textarea
      required={required}
      rows={4}
      className="w-full bg-[#1a1a1a] border border-[#333] rounded-lg px-4 py-3 focus:outline-none focus:border-[#FFB800] transition-colors resize-none"
      {...props}
    />
  </div>
);
```

### 6. ANIMATION UTILITIES

```javascript
// Fade in on scroll
const useFadeInOnScroll = (ref) => {
  useEffect(() => {
    const observer = new IntersectionObserver(
      ([entry]) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('animate-fade-in');
        }
      },
      { threshold: 0.1 }
    );

    if (ref.current) {
      observer.observe(ref.current);
    }

    return () => {
      if (ref.current) {
        observer.unobserve(ref.current);
      }
    };
  }, [ref]);
};

// Parallax effect
const useParallax = (ref) => {
  useEffect(() => {
    const handleScroll = () => {
      if (ref.current) {
        const scrolled = window.pageYOffset;
        ref.current.style.transform = `translateY(${scrolled * 0.5}px)`;
      }
    };

    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, [ref]);
};
```

### 7. CURRICULUM DATA STRUCTURE

```javascript
const curriculum = [
  {
    number: 1,
    title: "Intervju & Podcast",
    topics: [
      "osnove kadrova",
      "3 svetla",
      "rad sa sagovornikom",
      "dijalozi 2–3 osobe",
      "prelazak rampe (učenje)",
      "montažne tehnike (elipsa, simbol, metafora)"
    ]
  },
  {
    number: 2,
    title: "Reel & Reklama (Product Placement)",
    topics: [
      "brzina i ritam",
      "storytelling za mreže",
      "3 plana proizvoda",
      "beauty shot tehnike",
      "svetlo za reklamu"
    ]
  },
  {
    number: 3,
    title: "Cover & Muzički spot",
    topics: [
      "snimanje performansa",
      "ritmička montaža",
      "akcione sekvence",
      "kako snimiti šamar, udarac, pad",
      "speed ramp, slow motion"
    ]
  },
  {
    number: 4,
    title: "Video CV & Mini dokumentarac",
    topics: [
      "gluma pred kamerom",
      "lična prezentacija",
      "arhivska građa",
      "subjektivac",
      "improvizovano kretanje kamere",
      "izbegavanje praznog hoda",
      "making of vežba"
    ]
  },
  {
    number: 5,
    title: "Stop Motion & Eksperimentalni video",
    topics: [
      "animacija plastelinom",
      "metafore i simboli",
      "kreativni ritam",
      "color grading osnove"
    ]
  },
  {
    number: 6,
    title: "Priprema & Snimanje kratkog filma",
    topics: [
      "podela uloga",
      "dramaturgija",
      "3 dramska čvorišta",
      "akcija & reakcija",
      "plan snimanja",
      "snimanje timski"
    ]
  },
  {
    number: 7,
    title: "Projekcija, kritika, diplome i nagrade",
    topics: [
      "gledamo filmove",
      "profesionalna analiza",
      "nagrada za najbolji rad",
      "druženje i završna ceremonija"
    ]
  }
];
```

### 8. FAQ DATA STRUCTURE

```javascript
const faqs = [
  {
    question: "Da li treba da imam iskustva?",
    answer: "Ne."
  },
  {
    question: "Da li je telefon dovoljan?",
    answer: "Da — 1080p + Blackmagic app."
  },
  {
    question: "Šta ako ne znam da montiram?",
    answer: "Naučićeš tokom kursa."
  },
  {
    question: "Šta ako propustim čas?",
    answer: "Ne nadoknađuje se, ali dobijaš smernice."
  },
  {
    question: "Kada biramo uloge?",
    answer: "6. nedelja – po zaslugama."
  },
  {
    question: "Da li mogu doći pre 16 ili posle 50 godina?",
    answer: "Možeš — ako imaš disciplinu i želju."
  }
];
```

### 9. RESPONSIVE BREAKPOINTS

```javascript
// Tailwind breakpoints to use:
// sm: 640px
// md: 768px
// lg: 1024px
// xl: 1280px
// 2xl: 1536px

// Example usage:
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  {/* Content */}
</div>
```

### 10. FORM VALIDATION

```javascript
const validateForm = (data) => {
  const errors = {};
  
  if (!data.name) errors.name = "Ime i prezime je obavezno";
  if (!data.email) errors.email = "Email je obavezan";
  if (!data.phone) errors.phone = "Telefon je obavezan";
  if (!data.birthdate) errors.birthdate = "Datum rođenja je obavezan";
  if (!data.motivation) errors.motivation = "Motivacija je obavezna";
  if (!data.expectations) errors.expectations = "Očekivanja su obavezna";
  if (!data.consent) errors.consent = "Morate prihvatiti saglasnost";
  if (!data.rules) errors.rules = "Morate prihvatiti pravila";
  
  return errors;
};

const handleSubmit = async (e) => {
  e.preventDefault();
  const errors = validateForm(formData);
  
  if (Object.keys(errors).length === 0) {
    // Submit form
    try {
      // API call or email sending
      console.log("Form submitted:", formData);
      alert("Prijava uspešno poslata!");
    } catch (error) {
      console.error("Error submitting form:", error);
      alert("Greška pri slanju prijave. Pokušajte ponovo.");
    }
  } else {
    setFormErrors(errors);
  }
};
```

### 11. IMAGE PLACEHOLDERS

Use these Unsplash or placeholder URLs for development:

```javascript
const images = {
  hero: "https://images.unsplash.com/photo-1485846234645-a62644f84728?w=1920",
  camera: "https://images.unsplash.com/photo-1492619375914-88005aa9e8fb?w=800",
  lighting: "https://images.unsplash.com/photo-1516035069371-29a1b244cc32?w=800",
  studio: "https://images.unsplash.com/photo-1598488035139-bdbb2231ce04?w=800",
  instructor: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400",
  // Gallery images
  gallery1: "https://images.unsplash.com/photo-1579208575657-c595a05383b7?w=600",
  gallery2: "https://images.unsplash.com/photo-1598488035139-bdbb2231ce04?w=600",
  gallery3: "https://images.unsplash.com/photo-1536240478700-b869070f9279?w=600",
};
```

### 12. SMOOTH SCROLL IMPLEMENTATION

```javascript
const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId);
  if (element) {
    element.scrollIntoView({
      behavior: 'smooth',
      block: 'start'
    });
  }
};

// Usage in navigation
<button onClick={() => scrollToSection('application-form')}>
  Prijavi se
</button>
```

### 13. VIDEO EMBED TEMPLATE

```jsx
const VideoSection = () => {
  const [isPlaying, setIsPlaying] = useState(false);
  
  return (
    <section className="py-20 bg-[#0a0a0a]">
      <div className="container mx-auto px-4">
        <h2 className="text-4xl font-bold text-center mb-12">
          Pogledaj priču o avanturu
        </h2>
        <div className="max-w-4xl mx-auto">
          <div className="relative aspect-video bg-[#1a1a1a] rounded-lg overflow-hidden">
            {!isPlaying ? (
              <div className="absolute inset-0 flex items-center justify-center">
                <button
                  onClick={() => setIsPlaying(true)}
                  className="w-20 h-20 bg-[#FFB800] rounded-full flex items-center justify-center hover:scale-110 transition-transform"
                >
                  <Play className="w-10 h-10 text-black ml-1" />
                </button>
              </div>
            ) : (
              <iframe
                src="https://www.youtube.com/embed/VIDEO_ID?autoplay=1"
                className="w-full h-full"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowFullScreen
              />
            )}
          </div>
        </div>
      </div>
    </section>
  );
};
```

### 14. MOBILE MENU TEMPLATE

```jsx
const MobileMenu = ({ isOpen, onClose }) => (
  <div className={`fixed inset-0 bg-black/95 z-50 transform transition-transform ${
    isOpen ? 'translate-x-0' : 'translate-x-full'
  }`}>
    <div className="container mx-auto px-4 py-8">
      <button onClick={onClose} className="absolute top-4 right-4">
        <X className="w-8 h-8" />
      </button>
      <nav className="flex flex-col gap-6 mt-16">
        <a href="#about" className="text-2xl font-semibold hover:text-[#FFB800]">
          O kursu
        </a>
        <a href="#program" className="text-2xl font-semibold hover:text-[#FFB800]">
          Program
        </a>
        <a href="#pricing" className="text-2xl font-semibold hover:text-[#FFB800]">
          Cena
        </a>
        <a href="#contact" className="text-2xl font-semibold hover:text-[#FFB800]">
          Kontakt
        </a>
        <button className="bg-[#8B0000] px-6 py-3 rounded-lg text-xl font-semibold mt-4">
          Prijavi se
        </button>
      </nav>
    </div>
  </div>
);
```

### 15. FLOATING CTA BUTTON

```jsx
const FloatingCTA = () => {
  const [visible, setVisible] = useState(false);
  
  useEffect(() => {
    const handleScroll = () => {
      setVisible(window.scrollY > 500);
    };
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);
  
  return (
    <button
      className={`fixed bottom-8 right-8 bg-[#8B0000] text-white px-6 py-4 rounded-full shadow-lg hover:bg-[#A52A2A] transition-all transform ${
        visible ? 'translate-y-0 opacity-100' : 'translate-y-20 opacity-0'
      }`}
      onClick={() => scrollToSection('application-form')}
    >
      <span className="font-semibold">Prijavi se</span>
    </button>
  );
};
```

---

## USAGE INSTRUCTIONS

1. Copy the main FILMSKA_SKOLA_WEBSITE_SKILL.md file
2. Paste it into Claude's chat
3. Say: "Generate the complete React component for this film school website"
4. Claude will create a single .jsx file with all sections implemented
5. Customize images, video URL, and contact details as needed

## TESTING CHECKLIST

- [ ] All sections render correctly
- [ ] Responsive on mobile, tablet, desktop
- [ ] Form validation works
- [ ] Smooth scroll navigation
- [ ] Video embed functional
- [ ] Accordion/FAQ interactions work
- [ ] Hover effects present
- [ ] Color scheme matches brand
- [ ] Typography is readable
- [ ] Loading performance is acceptable

---

**This guide ensures Claude generates production-ready code with minimal follow-up needed.**
