
const contactForm = document.getElementById("contactForm");
const statusMessage = document.getElementById("status");

if (contactForm && statusMessage) {
  contactForm.addEventListener("submit", function (event) {
    if (!contactForm.checkValidity()) {
      event.preventDefault();
      contactForm.reportValidity();
      return;
    }

    statusMessage.textContent = "Sending your enquiry...";
  });
}


/* VantaVisa mobile navigation */
const vantaMenuButton = document.querySelector(".menu-toggle");
const vantaNavigation = document.querySelector(".navbar nav");

if (vantaMenuButton && vantaNavigation) {
  vantaMenuButton.addEventListener("click", function () {
    const isOpen = vantaNavigation.classList.toggle("open");

    vantaMenuButton.setAttribute("aria-expanded", String(isOpen));
    vantaMenuButton.textContent = isOpen ? "✕" : "☰";

    vantaNavigation.style.display = isOpen ? "flex" : "none";
    vantaNavigation.style.flexDirection = "column";
    vantaNavigation.style.gap = "16px";
    vantaNavigation.style.padding = isOpen ? "16px 0" : "0";
  });
}
/* Close VantaVisa menu after selecting a link */
if (vantaNavigation) {
  vantaNavigation.querySelectorAll("a").forEach(function (link) {
    link.addEventListener("click", function () {
      vantaNavigation.classList.remove("open");
      vantaNavigation.style.display = "none";

      if (vantaMenuButton) {
        vantaMenuButton.textContent = "☰";
        vantaMenuButton.setAttribute("aria-expanded", "false");
      }
    });
  });
}

/* VantaVisa application form confirmation */
const visaForm = document.getElementById("visaApplicationForm");
const formMessage = document.getElementById("formMessage");

if (visaForm && formMessage) {
  visaForm.addEventListener("submit", function (event) {
    if (!visaForm.checkValidity()) {
      event.preventDefault();
      visaForm.reportValidity();
      return;
    }

    formMessage.textContent = "Submitting your visa consultation request...";
    formMessage.style.color = "#176b43";
    formMessage.style.fontWeight = "600";
  });
}


/* Fix VantaVisa country application links */
document.querySelectorAll('a.country-link[href="#apply"]').forEach(function (link) {
  link.addEventListener("click", function (event) {
    event.preventDefault();

    const applicationForm = document.getElementById("apply");

    if (applicationForm) {
      applicationForm.scrollIntoView({
        behavior: "smooth",
        block: "start"
      });
    }
  });
});


/* VantaVisa: automatically select the country */
document.querySelectorAll(".country-card").forEach(function (card) {
  const applyLink = card.querySelector(".country-link");
  const heading = card.querySelector("h3");

  if (applyLink && heading) {
    applyLink.addEventListener("click", function () {
      const destination = document.getElementById("destination");
      if (!destination) return;

      const country = heading.textContent
        .replace(/[\u{1F1E6}-\u{1F1FF}]/gu, "")
        .trim()
        .toLowerCase();

      const countryMap = {
        "usa": "United States",
        "united states": "United States",
        "uk": "United Kingdom",
        "united kingdom": "United Kingdom",
        "canada": "Canada",
        "australia": "Australia",
        "germany": "Germany"
      };

      const targetCountry = countryMap[country];

      if (targetCountry) {
        destination.value = targetCountry;
        destination.dispatchEvent(
          new Event("change", { bubbles: true })
        );
      }
    });
  }
});
