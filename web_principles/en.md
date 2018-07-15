#  What Makes a Good Mobile Site?

![JennyGove](https://developers.google.com/web/images/contributors/jennygove.jpg)

**By** [ Jenny Gove ](https://developers.google.com/web/resources/contributors/jennygove)

Jenny Gove is a UX Research Lead at Google, where she conducts research on
smartphone experiences. She obtained her PhD from the University of
Southampton, UK.

Google and AnswerLab conducted a [research study](https://www.google.com/think/multiscreen/whitepaper-sitedesign.html?utm_source=web-fundamentals&utm_term=chrome&utm_content=ux-landing&utm_campaign=web-fundamentals) to answer this question.

> Mobile users are very goal-oriented. They expect to be able to get what they
need, immediately, and on their own terms.

The study was held through 119 hour-long, in-person usability sessions with
participants in the US. Participants were asked to perform key tasks across a
diverse set of mobile sites. iOS and Android users were included, and users
tested the sites on their own phones. For each site, participants were asked
to voice their thoughts aloud as they completed conversion-focused tasks like
making a purchase or booking a reservation.

The study uncovered 25 mobile site design principles, grouped into five
categories.

## Home page and site navigation

**Success:** Focus your mobile homepage on connecting users to the content they're looking for.

### Keep calls to action front and center

Make secondary tasks available through [menus](https://developers.google.com/web/fundamentals/design-and-ux/responsive/) or “below the fold” (the part of the webpage that can’t be seen without scrolling down).

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/hpnav-cta-good.png) 
**DO**: Make all of your users’ most common tasks easily available.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/hpnav-cta-bad.png) 
**DON'T**: Waste precious above-the-fold space with vague calls-to-action like “learn more”.

### Keep menus short and sweet

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/hpnav-menus-good.png) 
**DO**: Keep menus short and sweet.

Mobile users don't have the patience to scroll through a long list of
options to find what they want. Reorganize your menu to use as few items as
possible, without sacrificing usability.

### Make it easy to get back to the home page

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/hpnav-hp-good.png) 
**DO**: Make it easy to get back to the home page.

Users expect to go back to the homepage when they tap the logo in the top-left
of a mobile page, and they become frustrated when it isn't available or
doesn't work.

### Don't let promotions steal the show

Large app install interstitials (e.g., full-page promotions that hide content
and prompt users to install an app) annoy users and make it difficult to
perform tasks. In addition to annoying users, [sites that use interstitials
may see a negative impact to their search
rankings](https://webmasters.googleblog.com/2016/08/helping-users-easily-access-content-on.html).

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/hpnav-promo-good.png) 
**DO**: Promotions should be easily dismissable and not distract from the experience.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/hpnav-promo-bad.png) 
**DON'T**: Interstitials (sometimes called door slams) often annoy users and make using the site a pain.

## Site search

**Success:** Help mobile users find what they're looking for in a hurry.

### Make site search visible

Users looking for information usually turn to search, so the search field
should be one of the first things they see on your pages. Don't hide the
search box in a menu.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/ss-search-good.jpg) 
**DO**: Make search visible

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/ss-search-bad.jpg) 
**DON'T**: Hide search in overflow menus

### Ensure site search results are relevant

Users don't scan through multiple pages of results to find what they're
looking for. Make life easier on users by auto-completing queries, correcting
misspellings, and suggesting related queries. Rather than reinventing the
wheel, consider robust products like [Google Custom
Search](https://cse.google.com/cse/).

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/ss-relevant-good.png) 
**DO**: Macy's only returns kids items.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/ss-relevant-bad.png) 
**DON'T**: Return results for anything with the word kid in it.

### Implement filters to narrow results

Study participants rely on [filters](https://developers.google.com/custom-search/docs/structured_search) to find what they're looking for, and abandon
sites that do not have effective filters. Place filters above search results,
and help users by displaying how many results will be returned when a specific
filter is applied.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/ss-filters-good.jpg) 
**DO**: Make it easy to filter.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/ss-filters-bad.jpg) 
**DON'T**: Hide filter functionality.

### Guide users to better site search results

![Zappos guides users by asking them what they're looking
for.](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/ss-guide-good.png) 
**DO**: Help users to find what they're looking for by guiding them in the right direction.

For sites with diverse customer segments, ask a few questions before
presenting the search box, and use the customer's responses as search query
filters to ensure that users get results from the most relevant segment.

## Commerce and conversion

**Success:** Understand your customer journeys and let users convert on their own terms.

### Let users explore before they commit

Study participants were frustrated by sites that require upfront registrations
to view the site, especially when the brand was unfamiliar. Although customer
information may be integral to your business, asking for it too early may
result in fewer registrations.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/cc-gates-good.png) 
**DO**: Allow users to browse the site without requiring sign in.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/cc-gates-bad.png) 
**DON'T**: Place login or registration too early in a site.

### Let users purchase as guests

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/cc-purchase-guest-good.png) 
**DO**: Allow users to purchase with a guest account.

Study participants viewed guest checkouts as “convenient”, “simple”, “easy”, and “quick”. Users are annoyed by sites that force them to register for an account when making a purchase, especially when the benefit of an account is unclear.

### Use existing information to maximize convenience

Remember and [pre-fill preferences](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/#label-and-name-inputs-properly) for registered users. Offer
familiar, third-party checkout services for new users.

### Use click-to-call buttons for complex tasks

On devices with calling capabilities, [click-to-call links](https://developers.google.com/web/fundamentals/native-hardware/click-to-call/) enable users to make a phone call by simply tapping a link. On most mobile devices the user receives a confirmation before the number is dialed, or a menu is presented asking the user how the number should be handled.

### Make it easy to finish on another device
Users frequently want to finish tasks on other devices. For instance, they might wish to view an item on a larger screen. Or they might get busy and need to finish later. Support these customer journeys by enabling users to [share items on social networks](https://developers.google.com/web/fundamentals/discovery-and-monetization/social-discovery/), or by letting users email themselves links from directly within the site.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/cc-other-device-good.png) 
**DO**: Provide easy ways for users to continue browsing or shopping on another device.


## Form entry

**Success:** Provide a seamless, frictionless conversion experience with usable forms.

### Streamline information entry

Automatically advance to the next field when a user presses Return. In
general, the less taps the user must perform, the better.

### Choose the simplest input

Use the most [appropriate input type](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/choose-the-best-input-type) for each scenario. Use elements
like [`datalist`](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/choose-the-best-input-type#offer-suggestions-during-input-with-datalist) to provide suggested values for a field.

### Provide visual calendar for date selection

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/forms-calendar-good.png) 
**DO**: use calendar widgets when possible.

Clearly label start and end dates. Users should not need to leave a site and
check a calendar app just to schedule a date.

### Minimize form errors with labeling and real-time validation

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/forms-multipart-good.png) 
**DO**: Prepopulate content where possible.

Label inputs properly and validate input in real-time.

### Design efficient forms

Take advantage of
[autofill](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/#label-and-name-inputs-properly#use-metadata-to-enable-auto-complete) so that users can easily complete forms with pre-populated data.
Pre-fill fields with information you already know. For example, when
retrieving shipping and billing addresses, try to use
[`requestAutocomplete`](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/use-request-auto-complete) or enable users to copy their
shipping address to their billing address (or vice versa).

## Usability and form factor

**Success:** Delight your mobile users with small things that enhance their experiences.

### Optimize your entire site for mobile

Use a [responsive layout](https://developers.google.com/web/fundamentals/design-and-ux/responsive/) that changes based on the size and capabilities of the
user's device. Study participants found sites with a mix of desktop and
mobile-optimized pages even harder to use than desktop-only sites.

### Don't make users pinch-to-zoom

Users are comfortable with scrolling sites vertically, but not horizontally.
Avoid large, fixed-width elements. Use [CSS media queries](https://developers.google.com/web/fundamentals/design-and-ux/responsive/#use-css-media-queries-for-responsiveness) to apply different
stylings for different screens. Don't create content that only displays well
at a particular [viewport width](https://developers.google.com/web/fundamentals/design-and-ux/responsive/#set-the-viewport). Sites that force users to horizontally
scroll fail the [Google Mobile-Friendly Test](https://search.google.com/test/mobile-friendly), which may negatively
impact their search rankings.

### Make product images expandable

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/sw-make-images-expandable-good.png) 
**DO**: Make product
images expandable and easy to see detail.

Retail customers expect sites to let them [view high resolution closeups](https://developers.google.com/web/fundamentals/design-and-ux/responsive/images#make-product-images-expandable) of products. Study
participants got frustrated when they weren't able to see what they were
buying.

### Tell users which orientation works best

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/us-orientation.jpg) 
**DO**: Tell the user which orientation works best.

Study participants tended to stay in the same screen orientation until
something prompted them to switch. Design for both landscape and portrait, or
encourage users to switch to the optimal orientation. Make sure that your
important calls-to-action can be completed even if the users ignore the
suggestion to switch orientations.

### Keep your user in a single browser window

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/sw-single-browser-good.png) 
**DO**: Macy's keeps their users on their site by providing coupons on site.

Users may have trouble switching between windows and might not be able to find
their way back to the site. Avoid calls-to-action that launch new windows.
Identify any journeys that might cause a user to look outside your site and
provide features to keep them on your site. For example, if you accept
coupons, offer them directly on the site, rather than forcing users to search
other sites for deals.

### Avoid "full site" labeling

When study participants saw an option for a "full site" (i.e., desktop site)
versus a "mobile site", they thought the mobile site lacked content and chose
the "full" one instead, directing them to the desktop site.

### Be clear why you need a user's location

Users should always understand why you're asking for their
[location](https://developers.google.com/web/fundamentals/native-hardware/user-location/). Study participants trying to book a hotel in another
city became confused when a travel site detected their location and offered
hotels in their current city instead. Leave location fields blank by default,
and let users choose to populate them through a clear call-to-action like
"Find Near Me".

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/sw-navigation-good.png) 
**DO**: Always request access to location on a user gesture.

![](https://developers.google.com/web/fundamentals/design-and-ux/principles/images/sw-navigation-bad.png) 
**DON'T**: Asking for it immediately on the homepage as the site loads results in a poor user experience.






