# Case Studies API Documentation

## Overview
This documentation provides a detailed guide for the "case-studies" API endpoint. The endpoint handles complex case study data including layouts, images, testimonials, and various project-related information. The documentation is structured to help you understand how different fields work together to create a complete case study presentation.

## Base Fields
These fields form the foundation of every case study entry.

### Primary Information
1. **Title**
   - Type: `String`
   - Description: The main identifier for your case study
   - Usage: Appears as the primary heading in listings and headers
   - Example: `"Uspeak"`
   - Relations: Used to generate the `slug` field

2. **case_description**
   - Type: `String`
   - Description: Comprehensive overview of the project
   - Usage: Used in listings and preview cards
   - Example: `"Developed AI-driven platform enhancing communication skills through personalized feedback, UX design, and AI integration."`

### Layout Configuration
3. **layout**
   - Type: `String` (Enum)
   - Accepted Values: `"half"`, `"wide"`
   - Description: Controls the overall layout structure
   - Usage: Determines how content is displayed in listing pages
   - Note: Must be set to one of the accepted values for proper rendering

4. **imageHeight**
   - Type: `String` (CSS Class)
   - Description: Controls image container height
   - Usage: Applied to the main case study image
   - Example: `"md:h-[624px]"`
   - Related Fields: Works in conjunction with `imageWidth`

5. **textWidth**
   - Type: `String` (CSS Class) | `null`
   - Description: Controls text section width
   - Example: `"md:w-[28%]"`
   - Note: Can be null when using full-width layouts
   - Related Fields: Should be coordinated with `imageWidth`

6. **imageWidth**
   - Type: `String` (CSS Class) | `null`
   - Description: Controls image section width
   - Example: `"md:w-[72%]"`
   - Note: Should complement `textWidth` to create balanced layouts

7. **alignRight**
   - Type: `Boolean` | `null`
   - Description: Controls text alignment
   - Usage: When true, positions text on the right side
   - Note: Can be null for centered layouts

### Image Handling
8. **image**
   - Type: `String` (URL)
   - Description: Primary case study image
   - Example: `"http://localhost:1337/uploads/uspeak_aef98e46b6.jpeg"`
   - Usage: Main visual representation in listings

9. **case_thumbnail**
   - Type: `Array<Object>`
   - Description: Collection of thumbnail variations
   - Structure:
     ```javascript
     {
       id: number,
       name: string,
       alternativeText: string | null,
       caption: string | null,
       width: number,
       height: number,
       formats: {
         thumbnail: { name: string, url: string },
         small: { name: string, url: string }
       },
       url: string
     }
     ```
   - Note: Marked as optional but recommended for optimal display

10. **slug**
    - Type: `String`
    - Description: URL-friendly identifier
    - Example: `"uspeak"`
    - Usage: Used in routing and URLs
    - Relations: Generated from `Title` field

## Hero Section Fields
These fields control the prominent hero section of the case study page.

11. **herobottomtittle**
    - Type: `String`
    - Description: Hero section main title
    - Example: `"u Speak"`
    - Usage: Primary visual element in hero section
    - Relations: Should align with main `Title`

12. **herobackgroundSrc**
    - Type: `String` (URL)
    - Description: Hero background image
    - Example: `"http://localhost:1337/uploads/hero_81e0f6951a.png"`
    - Usage: Creates visual impact in hero section

13. **heroyearText**
    - Type: `String`
    - Description: Project year display
    - Example: `"2025"`
    - Usage: Temporal context in hero section

## Overview Section Fields
These fields structure the project overview section.

14. **overviewHeading**
    - Type: `String`
    - Description: Main overview section title
    - Example: `"USpeak Overview"`
    - Usage: Section identifier

15. **overviewSubheading**
    - Type: `String`
    - Description: Supporting headline
    - Example: `"Transforming Communication <br /> Skills with AI Technology"`
    - Note: Supports HTML tags for formatting

16. **overviewobjectiveTitle**
    - Type: `String`
    - Description: Objective section header
    - Example: `"Objective"`
    - Relations: Pairs with `overviewobjectiveText`

17. **overviewobjectiveText**
    - Type: `String`
    - Description: Detailed project objectives
    - Example: `"To develop an AI-driven platform designed to enhance communication skills through personalized feedback and interactive learning modules."`

18. **overviewbackgroundText**
    - Type: `String`
    - Description: Project context and background
    - Example: `"USpeak Inc. is a forward-thinking company specializing in AI-driven educational platforms..."`

## Results Section Fields
These fields showcase project outcomes.

19. **resultfinalImageSrc**
    - Type: `String` (URL)
    - Description: Final result visualization
    - Example: `"http://localhost:1337/uploads/12_6a57730d1e.png"`
    - Usage: Visual representation of project outcomes

20. **resultfinalParagraph**
    - Type: `String`
    - Description: Results summary
    - Example: `"The USpeak project was a significant success, achieving its objective of creating an engaging and effective platform for communication skills enhancement..."`

## Testimonial Fields
Client feedback and social proof section.

21. **testimonialText**
    - Type: `String`
    - Description: Client feedback quote
    - Example: `"USpeak's AI-driven platform revolutionized our team's communication skills..."`

22. **testimonialauthorName**
    - Type: `String`
    - Description: Testimonial provider name
    - Example: `"Martha"`
    - Relations: Links with `testimonialauthorPosition`

23. **testimonialauthorPosition**
    - Type: `String`
    - Description: Author's professional role
    - Example: `"Head of Training at Acme Corp"`

24. **testimonialauthorImageSrc**
    - Type: `String` (URL)
    - Description: Author's profile image
    - Example: `"http://localhost:1337/uploads/13_315a45b839.png"`

## Challenge and Solution Fields
These fields document project challenges and their resolutions.

25. **designchallanges**
    - Type: `Array<Object>`
    - Structure:
      ```javascript
      {
        id: number,
        title: string,
        description: string
      }
      ```
    - Example:
      ```javascript
      {
        "id": 16,
        "title": "Cross-Platform Compatibility",
        "description": "Ensuring consistent performance and design across different devices and screen sizes."
      }
      ```

26. **solution_overviews**
    - Type: `Array<Object>`
    - Structure: Matches `designchallanges`
    - Relations: Should address challenges listed in `designchallanges`

27. **design_thinkings**
    - Type: `Array<Object>`
    - Structure: Matches `designchallanges`
    - Usage: Documents design process steps

## Feature Documentation Fields
These fields showcase specific features and functionality.

28. **keyfeatures**
    - Type: `Array<Object>`
    - Structure:
      ```javascript
      {
        title: string,
        imageSrc: string,
        imageAlt: string,
        reversed: boolean,
        textWidth: string,
        imageWidth: string,
        imageHeightClass: string,
        bullet: string[]
      }
      ```
    - Example:
      ```javascript
      {
        "title": "Dashboard",
        "imageSrc": "http://localhost:1337/uploads/1_895f6c907b.png",
        "imageAlt": "iphone image",
        "reversed": false,
        "textWidth": "md:w-4/12",
        "imageWidth": "md:w-6/12",
        "imageHeightClass": "h-[450px]",
        "bullet": [
          "Comprehensive performance analytics presented in an easy-to-understand format.",
          "Sentiment analysis and detailed breakdowns of user scores."
        ]
      }
      ```

## Visual Design Fields
These fields document the visual design elements.

29. **illustrationbullets**
    - Type: `Array<Object>`
    - Structure:
      ```javascript
      {
        description: string
      }
      ```
    - Relations: Pairs with `illustration_images`

30. **illustration_images**
    - Type: `Array<Object>`
    - Structure:
      ```javascript
      {
        src: string,
        alt: string
      }
      ```

31. **visualelements**
    - Type: `Array<Object>`
    - Structure:
      ```javascript
      {
        Title: string,
        visualimagesrc: string,
        visualdescrption: string
      }
      ```
    - Usage: Documents typography, colors, and icons

## Results Documentation Fields

32. **resultrows**
    - Type: `Array<Object>`
    - Structure:
      ```javascript
      {
        imageSrc: string,
        imageAlt: string,
        imageContainerClasses: string,
        reversed: boolean,
        headingTop: string,
        headingBottom: string,
        bulletPoints: string[]
      }
      ```
    - Example:
      ```javascript
      {
        "imageSrc": "http://localhost:1337/uploads/10_eb8621aa2f.png",
        "imageAlt": "stats image",
        "imageContainerClasses": "h-[380px] md:h-[480px] lg:h-[580px]",
        "reversed": true,
        "headingTop": "Quantitative",
        "headingBottom": "Data",
        "bulletPoints": [
          "User engagement increased by 40% within the first three months post-launch.",
          "Average session duration improved by 25%.",
          "Subscription conversion rate increased by 15%."
        ]
      }
      ```

## Field Dependencies and Relationships

### Layout Dependencies
- `textWidth` and `imageWidth` should sum to 100% of container width
- `layout` affects how `imageHeight` and alignment fields are interpreted
- `reversed` fields in various sections should be coordinated for consistent layout flow

### Content Relations
1. Title Group:
   - `Title` → `slug` → `herobottomtittle`
   
2. Image Sets:
   - Main: `image` → `case_thumbnail`
   - Hero: `herobackgroundSrc`
   - Results: `resultfinalImageSrc`
   - Testimonial: `testimonialauthorImageSrc`

3. Overview Chain:
   - `overviewHeading` → `overviewSubheading` → `overviewobjectiveTitle` → `overviewobjectiveText`

4. Challenge-Solution Flow:
   - `designchallanges` → `solution_overviews` → `design_thinkings`

5. Visual Documentation:
   - `illustrationbullets` → `illustration_images` → `visualelements`

## Best Practices

1. Image Handling
   - Always provide `imageAlt` text for accessibility
   - Use consistent image dimensions within sections
   - Optimize images before upload

2. Content Structure
   - Maintain logical flow between related fields
   - Keep descriptions concise but informative
   - Use HTML formatting sparingly and consistently

3. Layout Configuration
   - Test layouts across different screen sizes
   - Ensure complementary width values
   - Use consistent spacing classes

4. Data Organization
   - Group related content in arrays
   - Maintain consistent ordering in lists
   - Use clear, descriptive titles
