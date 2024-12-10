Todo:

Add More Work Examples
Web Dev add a few small websites
Video Editing add Examples with iframes
expand blog page content
make navbar responsive
make blog page responsive

// Outline for blog process

A good approach is to store your posts in a structured, yet flexible JSON format. You’ll want each post to have a defined schema that includes essential metadata (like title, author, date) along with the main content and associated media. Since your workflow involves writing in Google Docs and copying the text over, consider placing the post’s main text in a single field that can handle a large chunk of content. For images, you can use inline references (like special tags) in the main text or maintain a separate array of image objects.

Example JSON Structure:

json
Copy code
{
  "posts": [
    {
      "id": "2024-01-15-new-years-reflections",
      "title": "New Year's Reflections",
      "author": "Jane Doe",
      "date": "2024-01-15",
      "tags": ["personal", "reflection", "holiday"],
      "summary": "Looking back on the past year and setting intentions for the new one.",
      "images": [
        {
          "id": "img-hero",
          "src": "/images/posts/new-years-reflections/hero.jpg",
          "alt": "A photo of a sunrise on January 1st"
        },
        {
          "id": "img-charts",
          "src": "/images/posts/new-years-reflections/resolutions_charts.png",
          "alt": "Graphs showing personal goals and achievements"
        }
      ],
      "content": "As the sun rose on January 1st, I couldn’t help but think back over the past year. {img:img-hero} The challenges, the triumphs, and the unexpected turns shaped who I am today. \n\nWhen I look at the goals I set for myself last year, I see a mixture of successes and areas for growth. {img:img-charts} These reflections help inform the intentions I set for the coming months—intentions focused on health, learning, and community."
    }
  ]
}
Key Points of This Structure:

Array of Posts:
posts is an array, making it easy to loop through and display multiple entries on your blog page.

Metadata Fields:

id: A unique identifier (often derived from the date and title) is useful for URLs and referencing.
title, author, date, tags, summary: These help you display and filter posts without parsing the entire content.
tags: Useful for organizing and categorizing content.
Images Array:
Store images in a dedicated images array, each with a unique id, src, and alt text. Keeping them separate from the main content ensures you have a centralized reference point for image metadata and easy reusability.

Content Field With Inline References:
The content field holds the main text, as copied and pasted from Google Docs (you might do minimal formatting or line breaks). Where you need images inside the text, insert a custom placeholder like {img:img-hero} corresponding to the id of the image in the images array.

When rendering the post on your site, you can replace {img:img-hero} with the appropriate <img> tag using the src and alt from the images array. This allows you to manage images outside the raw text, while still placing them wherever you like in the flow of the content.

Workflow:

Writing the Post:
Write your article in Google Docs. Once done, copy and paste the text into the content field of a new JSON post entry. Wherever you want an image to appear, insert a placeholder tag like {img:uniqueID} in the doc, which you’ll later align with an entry in the images array.

Local Images:
Store your images locally (e.g., public/images/posts/new-years-reflections/hero.jpg). Define them in the images array, giving each one a unique id and referencing that ID in the content.

Rendering on the Website:
Your frontend code can:

Fetch the JSON file (e.g. fetch('/data/posts.json')).
Loop through posts to build the blog index or a specific post page.
For each post’s content, search for {img:someID}, find the corresponding image object, and replace the placeholder with an <img> element.
Benefits of This Approach:

Simplicity:
The bulk of your post is just a single string field, making it easy to copy/paste directly from Google Docs.

Flexibility:
Inline image references allow you to place images anywhere in the text without messy HTML or markdown in the JSON itself.

Separation of Concerns:
Keeping images metadata separate but referencing them in content placeholders makes it easier to update image paths, alt text, or even switch image formats later, without having to edit the main content repeatedly.

This structure should give you a clean, maintainable solution for managing blog posts in JSON, allowing you to write in Google Docs and then translate that directly into your site’s blog format.