## Design Journal — Navigation, Texture, and Visual Hierarchy  
**Dates:** _[add dates if you want]_  

Over the past two days, I focused on stabilizing and refining the visual architecture of my portfolio—specifically the relationship between background texture, navigation structure, and image presentation.

### Background & Surface Logic  
A major portion of this work involved diagnosing why my intended background texture was not appearing consistently across pages. After ruling out caching and CSS override issues, I discovered the root cause was a simple but consequential file mismatch: the texture file was a `.png`, not a `.jpg`. Correcting this immediately restored the textured background across non-landing pages.

This moment reinforced how fragile surface logic can be on the web—small discrepancies in file naming or paths can collapse an entire visual layer. Once resolved, the texture began functioning as intended: a unifying substrate behind the navigation and gallery content, providing depth without competing with the work itself.

### Navigation Structure: Long Horizontal Cards  
I intentionally retained the long, horizontal navigation cards rather than converting them into a grid or carousel. These cards function less like thumbnails and more like visual banners—each one acting as a threshold into a body of work rather than a discrete object.

Much of the refinement here focused on **image vibrancy**. Initially, the images felt muted and over-controlled due to layered overlays and conservative contrast. I addressed this by:
- Increasing saturation, contrast, and brightness directly on the card background images
- Reducing the opacity and weight of the gradient overlays that were dulling color
- Preserving legibility by subtly isolating text areas rather than darkening the entire image

This allowed the images to feel more present and energetic without sacrificing readability.

### Separating Navigation from Gallery Experience  
While working through layout options, I clarified an important structural distinction:  
- **Navigation pages** should remain focused, directional, and visually bold  
- **Gallery pages** should prioritize looking, lingering, and contextual reading  

Rather than forcing navigation pages into gallery-like behavior (e.g., carousels), I designed a separate gallery pattern: a grid of works that open into a modal/lightbox with expanded images and optional process notes. This separation preserves clarity of intent—navigation as orientation, galleries as immersion.

### Current State  
At the end of this iteration:
- The textured background is consistent and intentional across pages
- Navigation cards are visually stronger and more vibrant
- The site’s structure more clearly distinguishes between *entry points* and *artwork spaces*
- I have a flexible, non-carousel gallery system ready for use where deeper engagement is needed

Overall, this phase was less about adding features and more about aligning visual systems—ensuring that background, image treatment, and layout hierarchy support the work rather than competing with it.
