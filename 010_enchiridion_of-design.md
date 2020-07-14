# Enchiridion of Design

## Feature Design

* Start with a feature, not a layout. Because an app is a collection of
features. Before you have designed a few features, you don't even have the
information you need to make a decision of how the app shell (navigation,
                                                              sidebar, page
                                                              content)
should work.

* Instead of shell start with a piece of functionality. You are building an OKR
software. Start with the OKR box and the features it needs like objective name,
key result names, progress bar, inputs.

* When you develop a new feature, don't hung up making low-level decisions about
things like typefaces, shadows, icons. Use default browser styling.

* Design in grayscale and find the right spacing and sizing first.

* The goal is to move fast.

* Don't design every single feature in an app before you move on to
implementation. Don't cover edge cases like how the screen looks with 5000
contacts, or how to display an error message in the form, how the calendar
should look if there are two events scheduled at the same time.

* Start to design a simple version of the next feature you want to build.

* Don't imply functionality in your designs that you aren't ready to build.
  * For example you are building an OKR form, if user cannot archive it in the
first version, don't add the archive button, or if a user cannot edit it in the first version don't
add an edit button.

* It's better to have a simple feature avaiable than no feature at all.

* Building features is hard, designing the smallest useful version you can ship
reduces that risk considrably not to ship at all because you made it too
complicated.

* DT: Use progressive enhancement approach for building software: 1) identify
the core functionality, 2) build it with the simplest technology possible, 3)
enhance.

## Choose a personality
* Choose a personality for your design. A banking app might try to communicate
secure and professional, a trendy startup migh have a disgn that feels fun and
playful (slack).

* Font plays an important role how the design looks. For elegant and classic
look choose serif. For playful look, use rounded sans serif, for plainer look
use neutral sans serif.

* Color: blue is safe and familiar, gold is expensive, pink is more fun. You can
use psychological frameworks or simply pick what you think most resonates with
the personality chosen.

* Border radius: small border radius is neutral, large border radius feels more
playful, no border radius feels more serious or formal.

* Language: Choose the right personal tone. Casual language makes a site feel
frendlier.

## On choices

* Avoid analysis/paralysis and start with a smaller set of options for color
shades, limit to 10 shades, font-size limit to 10 sizes (use modular scale),
limit color to a single color palette.

* When you are designing using a constrained set of values, decision-making is a
lot easier because there are a lot fewer "right" choices. For example you are
choosing a size for an icon. Define the sizing scale in advance 12px, 16px, 24px
and 32px. To pick the best option, start by taking a guess at which one will
look best, maybe 16px. Then try the value on either side 12px and 24px for
comparison.

* Systemize everything, the more system you have the faster you will be albe to
work: Font-size, font-weight, line-height, color, margin, padding, width,
height, box shadows, border radius, opacity etc..

* Look for opportunities to introduce new systems as you make new decisions, and
try to avoid havint to make the same low-level decisions twice.

## Hierarchy

* One of the biggest factors in making something "look good" has nothing to do
with superficial styling at all.

* Visual hierarchy refers to how important the elements in an interface apper in
relation to one another, and it's the most effective tool you have for making
something feel "designed"

* When everything in an interface is competing for attention, it feels noisy and
chaotic.

* When you de-emphasize secondary and tertiary information, and make an effort
to highlight the elements that are most important, the design will be more
pleasing.

* Use not only the font-size but also try using font weight and color.

* Stick to three colors:
  1. A dark color for primary content (headline)
  2. A grey for secondary content (date on articles)
  3. A lighter grey for teriary content (copyright in footer)

* Stick to two font-weights:
  1. A normal font weight (400 or 500) for most text
  2. A heavier font weigh (600 or 700) for text you want to emphasize

* Stay away from fonts under 400 for UI

* Don't use grey text on colored backgrounds

* Making the text closer to the background is what creates the hierarchy

* Choose the color with the same hue of a background and adjust the saturation
and lightness until it looks right to you.

* Emphasize by de-emphasizing, instead of trying to further emphasize the
element you want to draw attention to, figure out how you can de-emphasize the
elements that are competing with it.

* For example if you feel like the sidebar is competing with the main content,
don't give it a background color.

* Combine labels and values, for example if you need to display invetory instead
of "In stock: 12", try "12 left in stock".

* Or real estate app instead of Bedrooms: 3 Bathrooms: 2, use something like 3
Bedrooms and 2 Bathrooms.

* Use labels only in forms! Or if you need it, try to de-emphasize the label by
making it smaller, reducing the contrast, using a font weight, or some
combination of all three.

* For interfaces where the user will look at labels, it might be sense to
emphasize the label instead of the data. For example the user wants to find the
resolutions of a monitor he will be probably scanning the page for words like
"resolution" and not 3200x1200?

* Bold text feels emphasized compared to regular text is that bold text convers
more surface area.

* Just like bold text, icons are generally "heavy" and cover a lot of surface
area. As a result, an icon next to some text tends to feel emphasized. Unline
text there is no way to change the "weight", so to create balance it needs to be
de-emphasized by lowering the contrast of the icon by giving it a softer color.

* Reducing the contrast works like a counterbalance, making heavier elements
feel lighter even though the weight hasn't changed.

* Semantics are secondary. Semantics in button design are important, but that
doesn't mean you can forget about hierarchy.

P.60

* Source: https://refactoringui.com/

