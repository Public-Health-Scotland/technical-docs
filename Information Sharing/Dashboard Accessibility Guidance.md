# Dashboard Accessibility Guidance

*Adapted from guidance originally written by the PHS Statistics Publications Team, Public Health Scotland. Also available on [The Spark](https://spark.publichealthscotland.org/corporate-guidance/accessibility-branding-and-style/).*

* [General guidance](#general-guidance)
* [Automated testing tools](#automated-testing-tools)
* [Code](#code)
* [Keyboard navigation](#keyboard-navigation)
* [Links](#links)
* [Images used within dashboards](#images-used-within-dashboards)
* [Chart design and layout](#chart-design-and-layout)
* [Branding and corporate colours](#branding-and-corporate-colours)
* [Alternative formats](#alternative-formats)

## General guidance

Consider the overall layout and usability of the dashboard. Dashboards should ideally not contain commentary and masses of text, they should be used as tools to allow users to interact with your data, alongside web pages that contain any commentary. Consult with the content design team for advice around this via [phs.statspublications@phs.scot](mailto:phs.statspublications@phs.scot).

### Top Tips

* Try to minimize large areas of white space.
* Think about the tabbing/focus order whilst using a keyboard to navigate your dashboard. Make sure you can navigate using a keyboard only, in a logical order.
* Think about where users expect to find certain information – such as instructions, data sources, and contact information.
* Try not to repeat content unnecessarily.
* Perform UX testing with people not familiar with the dashboard or data.
* Do not use italics or underline text for emphasis.

## Automated testing tools

There are a number of tools available for testing accessibility. Amongst the most useful are, including:

* Chrome browser extensions:
  * The [axe browser extension](https://www.deque.com/axe/browser-extensions/) is useful for running automated and guided tests on targeted web pages. Signing up to axe beta allows you to export results and run all automatic tests.
  * The [WAVE browser extension](https://wave.webaim.org/extension/) can be used to run automated tests in an easy-to-view format.
  * [Lighthouse tool](https://developers.google.com/web/tools/lighthouse)
  * [Accessibility Insights](https://accessibilityinsights.io/en/downloads/) tools for a variety of platforms, not just Chrome.
* Portable [NVDA screen reader](https://www.nvaccess.org/download/)
* [NU HTML parser](https://validator.w3.org/nu/)
* DevTools (F12)

## Code

* Ensure that the language attribute is set to “en” (see [Language of page WCAG 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)).
* Ensure the main heading is marked up as such (see [Info and relationships WCAG 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)), this is particularly important for each new “tab” or “page” you build within the dashboard.
* Headers (H1 to H6) should be used to denote content levels, not as a convenient way to style text.
* Header levels should start at H1 and proceed in order as appropriate – for example, don’t start at H2, with no H1 or don’t jump from H1 to H3.
* The visual appearance of headers should match the programmatic level – for example, H1 should appear more prominent than H2.
* Ensure that buttons are correctly labelled and are not empty (see [Link purpose (in context) WCAG 2.4.4](https://webaim.org/standards/wcag/checklist#sc2.4.4)).
* Be careful with your placement and use of hover tooltips. We have encountered dashboards with tooltips used that are disorientating for the user (see [Content on hover or focus WCAG 1.4.13](https://www.w3.org/WAI/WCAG21/Understanding/content-on-hover-or-focus.html) for more guidance on creating tooltips or popups).
* Ensure that you have complete start and end tags, and these are nested according to specification. This helps ensure that assistive technologies can parse the content accurately and without crashing. It is also important to ensure IDs are unique not duplicated (see [Parsing WCAG 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)).
* All interface components must have accessible names. This includes (but not limited to) containing frames, information buttons, labels, <div> elements (see [Name, role, value WCAG 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html) for more guidance on building interface components).
* Be mindful of any time limits applied to dashboards, where users become disconnected from the server after a set period of time (see [Timing adjustable WCAG 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html))

## Keyboard navigation

* Users must be able to interact with the dashboard using only a keyboard (see [Keyboard WCAG 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html))
* Any function that can be performed using a mouse must also be available to a keyboard-only user. For example:
  * interacting with a plot to download as an image or to zoom in (see [Reflow WCAG 1.4.10](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html) for more information on the importance of being able to enlarge content displayed on the page)
  * dismissing content – hover text, closing pop-ups
* Navigation should be possible using only standard keys on a keyboard:
  * tab
  * enter
  * arrows
  * shift
  * escape
* There should be a logical order to the tabbing sequence – this can be tested using tab (forwards) and shift-tab (backwards). You want to ensure that elements within the dashboard are focussed on in a logical order (see [Focus order WCAG 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)).
* Check that any drop-down menus or pop-outs can also be navigated using this method.
* There should be a means to navigate back to the original page.
* Guidance for using inputs should be added. This guidance should be placed before the input object to be read by screen readers before the user encounters the object.

## Links

* All links should be encoded correctly as links (see [Name, role, value WCAG 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)).
* When writing a link, make it descriptive and front-load it with relevant terms instead of using something generic like ‘click here’ or ‘more’. Generic links do not make sense out of context or tell users where a link will take them. They also do not work for people using screen readers, who often scan through lists of links to navigate a page. It’s important the links are descriptive so they make sense in isolation.
  * Bad: For further information click here.
  * Good: View more information on good link practice.
* Do not use the same link text to link to different places.
* Think about the size of the link users need to select. For users with reduced motor skills, a one-word link could be very difficult to select.
* Avoid the use of images as links. If unavoidable, ensure that the image has alt text with details of the link. For example, an image of the PHS logo that links to the PHS homepage would fail accessibility as it would be announced to a screen reader as “PHS logo, link” without saying where the link goes. This could be improved by providing alt-text to state that this will redirect to the homepage.
* If staying on the embedded dashboard, the link should open in the same window. If leaving the site or dashboard, the link should open in a new window. This should be made clear to the user by text explanation in the title tag. As an example, moving from one tab to another is an internal link, and linking to any other website is external. 
* Confirm the title tag does not overwrite link text and provide an example of code.

## Images used within dashboards

* Decorative images should not be used as this does not aid in understanding content.
* Images should display correctly and not be cropped or stretched. Image dimensions should match the code settings for display.
* Do not create text as images as these will not be discernible to a screen reader (see [Images of text WCAG 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html))
* Images should have alternate text (see [non-text content WCAG 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html) for more information).
* Alt text should typically:
  * Be accurate and equivalent in presenting the same content and function as presented by the image.
  * Be succinct. This means the correct content and function of the image should be presented as succinctly as is appropriate. Typically no more than a few words are necessary, though rarely a short sentence or two may be appropriate.
  * NOT be redundant or provide the exact same information as text within the context of the image.
  * NOT use the phrases "image of ..." or "graphic of ..." to describe the image. It’s usually apparent to the user that it is an image. And if the image is conveying content, it is typically not necessary that the user knows that it is an image that is conveying the content, as opposed to text.

## Chart design and layout

* All chart elements should have sufficient colour contrast (see [Contrast (minimum) WCAG 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)).
  * Make sure your chart works in greyscale.
  * Blue is a rich colour across types of colour blindness so is a good base colour for charts.
* If gridlines are to be used in graphs, they should always be grey. A good tone is #bebebe (R190 G190 B190).
* Dashed lines can be used for graphs but no more than two variations.
* Avoid pattern fill.
* Charts should have horizontal text, never vertical. Consider swapping the chart axis if long labels are a problem.
* Double value axes should not be used. Use two charts instead.
* Include instructions for interacting with charts.
* Chart titles should be coded as text, not as images. Include a title above the chart to ensure that this is read by a screen reader prior to the chart.
* Output resolution should be set to take account of intended destination. If a chart is pasted from Excel into Word and resized, the image can become pixelated and font size can fall below required size.
* Ensure that chart elements will not be clipped or hidden when users change display options – for example, text spacing, resolution, resizing, contrast (see [Reflow WCAG 1.4.10](https://www.w3.org/WAI/WCAG21/Understanding/reflow.html) for more guidance, particularly around avoiding losing functionality beyond 400% zoom).
* Do not do the following:
  * use colour alone to convey information (see [Use of colour WCAG 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)). Alternative options include:
    * adding labels
    * mapping values to shapes
    * splitting up charts
  * use subtle colour changes to indicate extreme outliers
  * rely solely on sensory characteristics of components such as shape, color, size, visual location, orientation, or sound (see [Sensory characteristics WCAG 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html))
  * have internal scroll bars on large chunks of text o use borders and backgrounds for charts
  * use text that is too small
  * use white space/images as padding
  * map tool tips underlinked like links when they are not links.

## Branding and corporate colours

The logo must be presented in accordance with PHS branding guidelines and style guide. The Public Health Scotland logo should be used. Logos of legacy organisations should not be used.

### Colour palette for digital products

#### Main colour palette (HEX)

|                | **Purple** | **Magenta** | **Blue** | **Green** |
|----------------|------------|-------------|----------|-----------|
| **HEX**        | #3F3685    | #9B4393     | #0078D4  | #83BB26   |
| **TINT - 80%** | #655E9D    | #AF69A9     | #3393DD  | #9CC951   |
| **TINT - 50%** | #9F9BC2    | #CDA1C9     | #80BCEA  | #C1DD93   |
| **TINT - 30%** | #C5C3DA    | #E1C7DF     | #B3D7F2  | #DAEBBE   |
| **TINT - 10%** | #ECEBF3    | #F5ECF4     | #E6F2FB  | #F3F8E9   |

#### Main colour palette (RGB)

|                | **Purple**   | **Magenta**  | **Blue**     | **Green**    |
|----------------|--------------|--------------|--------------|--------------|
| **HEX**        | 63,54,133    | 155,67,147   | 0,120,212    | 131,187,38   |
| **TINT - 80%** | 101,94,157   | 175,105,169  | 51,147,221   | 156,201,81   |
| **TINT - 50%** | 159,155,194  | 205,161,201  | 128,188,234  | 193,221,147  |
| **TINT - 30%** | 197,195,218  | 225,199,223  | 179,215,242  | 218,235,190  |
| **TINT - 10%** | 236,235,243  | 245,236,244  | 230,242,251  | 243,248,233  |

#### Supporting colour palette (HEX)

|                | **Graphite** | **Teal** | **Liberty** | **Rust** |
|----------------|--------------|----------|-------------|----------|
| **HEX**        | #948DA3      | #1E7F84  | #6B5C85     | #C73918  |
| **TINT - 80%** | #A9A4B5      | #4B999D  | #897D9D     | #D26146  |
| **TINT - 50%** | #CAC6D1      | #8FBFC2  | #B5AEC2     | #E39C8C  |
| **TINT - 30%** | #DFDDE3      | #BCD9DA  | #D3CEDA     | #EEC4BA  |
| **TINT - 10%** | #F4F4F6      | #E9F2F3  | #F0EFF3     | #F9EBE8  |

#### Supporting colour palette (RGB)

| **null**       | **Graphite** | **Teal**     | **Liberty**  | **Rust**     |
|----------------|--------------|--------------|--------------|--------------|
| **HEX**        | 148,141,163  | 30,127,132   | 107,92,133   | 199,57,24    |
| **TINT - 80%** | 169,164,181  | 75,153,157   | 137,125,157  | 210,97,70    |
| **TINT - 50%** | 202,198,209  | 143,191,194  | 181,174,194  | 227,156,140  |
| **TINT - 30%** | 223,221,227  | 188,217,218  | 211,206,218  | 238,196,186  |
| **TINT - 10%** | 244,244,246  | 233,242,243  | 240,239,243  | 249,235,232  |

## Alternative formats

* Provide a download option for data in a flat format, for example csv.
* If a chart is displayed, the option to hide or show and download the displayed data (after any selecting or filtering has taken place) should also be provided.
* Table cells should be accessible via keyboard (tab).
