| [home page](https://naynikaw.github.io/nayn-viz/) | [data viz examples](dataviz-examples) | [critique by design](critique-by-design) | [final project I](final-project-part-one) | [final project II](final-project-part-two) | [final project III](final-project-part-three) |

# Critique by Design: Where's the Strongest Coffee?

As a CMU student who relies heavily on coffee to power through long study sessions and late-night coding marathons, I've always been curious about which coffee chains actually deliver the most caffeine. When I found a visualization comparing caffeine content across UK high street coffee chains, I immediately saw an opportunity to transform confusing data into actionable insights. This redesign journey took me from a static table that buried its most interesting findings to a visual story that reveals surprising patterns at a glance.

Through this process, I learned that good data visualization isn't just about making information pretty—it's about making the right comparisons visible and removing barriers between viewers and insights. What started as a critique of a simple table evolved into a deep exploration of how we normalize data, incorporate user feedback, and design for real decision-making moments.

## Step one: the visualization

![Original Coffee Caffeine Visualization](/original-coffee-viz.png)

**Source:** [Include actual source - MakeoverMonday or original article link]

I selected this visualization because it combines personal relevance with clear design flaws that create an excellent redesign opportunity. As someone who drinks multiple cups of coffee daily while working on data science projects, understanding caffeine content across chains directly impacts my health and purchasing decisions. 

What immediately caught my attention was how difficult it was to answer a simple question: "Which chain has the strongest coffee?" The data was all there—caffeine amounts, drink sizes, multiple chains and products—but extracting meaningful comparisons required mental gymnastics. I found myself staring at numbers like "Pret: 180mg (30ml)" and "Starbucks: 33mg (25ml)" trying to figure out which was actually stronger. This cognitive friction signaled a fundamental design problem.

The visualization also represents a common real-world scenario: health-relevant consumer data that needs to support quick decision-making but is presented in a format that demands analysis. I saw potential to transform this from a data dump into a tool that actually helps people make informed choices standing in a coffee shop line.

## Step two: the critique

Using Stephen Few's Data Visualization Effectiveness Profile, I systematically evaluated the visualization across seven dimensions. This structured approach revealed specific weaknesses I might have missed with a more casual critique.

**Key findings from the critique:**

The visualization's most critical flaw is **poor perceptibility** (rated 4/10). Tables force viewers to scan rows and columns repeatedly, holding multiple numbers in working memory. There's no visual encoding—no color, no sorting, no spatial arrangement—to help identify patterns. Comparing any two values requires conscious effort rather than immediate visual recognition.

The second major issue is **misleading truthfulness** (rated 8/10 for accuracy but problematic for fairness). While the numbers themselves are accurate, comparing raw milligram amounts across vastly different volumes (25ml to 362ml) creates false equivalencies. Pret's espresso shows 180mg total, which appears similar to their 180mg cappuccino—but the espresso is in 30ml while the cappuccino is in 350ml, making the espresso 12x more concentrated. This isn't lying with data, but it's presenting it in a way that obscures the truth about comparative strength.

**Engagement** was particularly weak (3/10). The visualization presents data without insight—there's no title asking a question, no highlighted finding, no narrative. The most compelling story in this data (Pret's espresso is 4.5x stronger than Starbucks') is completely buried, requiring viewers to calculate it themselves.

Comparing Few's method to the Good Charts approach from previous assignments, I found Few's framework more valuable for this redesign because it forced me to articulate specific problems ("poor perceptibility due to table format requiring systematic scanning") rather than general impressions ("hard to read"). The Good Charts method's emphasis on "truthful, functional, beautiful" provides a quicker assessment tool, but Few's seven categories helped me identify exactly which aspects needed redesign and why.

The critique made one thing crystal clear: the missing normalized metric (caffeine per unit volume) was the linchpin issue. Without it, all other improvements would be superficial.

## Step three: Sketch a solution

Based on the critique insights, I knew my redesign needed to accomplish three things: normalize caffeine by volume, use visual encoding instead of tables, and organize information to match user decision-making.

![Wireframe Sketch](/coffee-wireframe-sketch.png)

**My initial sketch approach:**

I designed a three-panel horizontal bar chart, with each panel representing a drink type (Espresso, Cappuccino, Filter Coffee). Within each panel, chains are sorted from highest to lowest caffeine concentration (mg per 100ml). I used hatched bars to indicate relative strength and included numeric labels for precise comparisons.

**Key design decisions in the sketch:**

**Normalized metric:** I created a calculated field for caffeine per 100ml because this is the only fair way to compare "strength." A 30ml espresso with 180mg is far more concentrated than a 350ml cappuccino with 180mg, and viewers shouldn't need to calculate this themselves.

**Three-panel layout:** I separated drink types into distinct panels rather than using grouped bars or a single chart. My reasoning was that consumers typically decide on a drink type first ("I want an espresso" or "I want a cappuccino"), then choose which chain to visit. This layout matches the actual decision-making process.

**Sorted bars:** Arranging chains from highest to lowest concentration within each panel makes competitive rankings immediately visible. Instead of scanning back and forth to find maximums, the answer is always at the top of each panel.

**Handling missing data:** I explicitly labeled "No Data Available" for chains without filter coffee rather than omitting them entirely. This transparency shows these chains were included in the analysis but don't offer that product.

I also sketched alternative approaches—a slope chart showing how concentration drops from espresso to cappuccino to filter coffee for each chain, and a scatter plot with volume on the x-axis and total caffeine on the y-axis. However, I felt these alternatives didn't answer the core question ("which chain has the strongest [drink type]?") as directly as the three-panel bar chart.

## Step four: Test the solution

I prepared a testing script focusing on comprehension and usability rather than leading questions. I wanted to know if my redesign actually made the information more accessible.

**Questions I asked:**
- Can you tell me what you think this is?
- Can you describe to me what this is telling you?
- Is there anything you find surprising or confusing?
- Who do you think is the intended audience for this?
- Is there anything you would change or do differently?

**Results:**

| Question | Interview 1 (Male, mid-20s, MISM student) | Interview 2 (Female, mid-20s, MISM student) |
|----------|-------------|-------------|
| What is this? | "Comparing caffeine levels across coffee chains—Pret, Starbucks, etc." | "Coffee strength comparison. Different chains, different drinks." |
| What's it telling you? | "Pret has the strongest espresso, Starbucks is weak across the board. It's showing concentration, not just total caffeine." | "If I want strong coffee, go to Pret for espresso. If I want weak coffee, Starbucks. The middle is cappuccinos." |
| Anything surprising/confusing? | "Pret's bar is massive compared to others—didn't expect that. Confused why Caffè Nero has 'No data' but then has a bar with stripes? Inconsistent." | "Yeah, why is Caffè Nero at bottom of filter coffee with a bar when Costa says 'No data'? Either both should be missing or both should have bars." |
| Intended audience? | "Coffee drinkers who care about getting the most caffeine. Maybe students pulling all-nighters." | "People in UK maybe? These are UK chains. Someone deciding where to get coffee before an exam or work." |
| What would you change? | "The bars don't have numbers. I can't tell exact values. Also, what's 'normal' caffeine? Is 600 mg/100ml dangerous? Give me context." | "Put actual numbers on the bars. I want to know if Costa is 90 or 95. Also, color would help—maybe red for high caffeine, green for low. The hatching is hard to distinguish." |

**Synthesis:**

Both interviewees grasped the core concept immediately—they understood it was comparing coffee strength across chains and could identify basic patterns (Pret strongest, Starbucks weakest). This validated my three-panel layout and sorted arrangement.

However, a clear pattern emerged: **both strongly requested numeric labels on the bars**. While the bar lengths showed relative comparisons, viewers wanted precise values for close calls (like Costa vs Greggs in cappuccinos). This was my biggest oversight—I had assumed visual comparison would be sufficient, but users wanted both visual and numeric precision.

The second consistent feedback point was **requesting color differentiation**. Both mentioned that hatching alone wasn't enough to distinguish strength levels, especially for similar values. They suggested a gradient (red = strong, green/yellow = weak) or categorical coloring.

The **inconsistent handling of missing data** confused both interviewees. In my sketch, I had accidentally shown Caffè Nero with both "No data" annotation and a partial bar in filter coffee, while Costa just had the annotation. This inconsistency made them question whether the data was actually missing or just displayed incorrectly.

**Changes for final redesign:**

Based on this feedback, I committed to three modifications:
1. **Add numeric labels to every bar** showing the exact concentration value
2. **Implement a color gradient** (in shades of brown) where darker = higher concentration
3. **Standardize missing data representation**—explicitly show "No Data Available" annotations consistently

I also noted the request for health context (daily limits, what's "normal") but decided to address this through a caption rather than adding reference lines to the chart itself, which might create visual clutter.

## Step five: build the solution

<div class='tableauPlaceholder' id='viz1763091737640' style='position: relative'><noscript><a href='#'><img alt='Where&#39;s the Strongest Coffee?Caffeine Concentration by High Street Chain (mg per 100ml) ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Co&#47;Coffee_17630901956420&#47;Sheet1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Coffee_17630901956420&#47;Sheet1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Co&#47;Coffee_17630901956420&#47;Sheet1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /><param name='filter' value='publish=yes' /></object></div>                  
<script type='text/javascript'>                    
  var divElement = document.getElementById('viz1763091737640');                    
  var vizElement = divElement.getElementsByTagName('object')[0];                    
  vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    
  var scriptElement = document.createElement('script');                    
  scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                  
  vizElement.parentNode.insertBefore(scriptElement, vizElement);                
</script>

The final visualization successfully transforms the original table's buried insights into an immediately comprehensible story about coffee strength across UK chains.

**What the redesign shows:**

The three-panel horizontal bar chart reveals patterns that were completely hidden in the table format. Most strikingly, Pret's espresso concentration of 600 mg/100ml—rendered in deep red—dominates the espresso panel, making it visually obvious that Pret's espresso is exceptionally strong. The numeric label confirms it's 4.5x more concentrated than Starbucks' 132 mg/100ml.

In the cappuccino panel, Costa emerges as the leader at 90 mg/100ml, which surprised me given Pret's espresso dominance. This reveals that chains have different strategies: Pret maximizes espresso strength while Costa balances strength across milk-based drinks. Starbucks appears consistently at the bottom of every panel, showing their standardization strategy prioritizes consistency over high caffeine.

The filter coffee panel shows interesting missing data—Costa and Caffè Nero don't offer filter coffee, suggesting these premium chains focus exclusively on espresso bar drinks. Among chains that do offer it, Pret (77) and Greggs (66) deliver similar concentrations, while Starbucks (29) again ranks lowest.

**Design decisions:**

I created a calculated field in Tableau: `([Caffeine (mg)] / [Drink size (ml)]) * 100` to generate the mg per 100ml metric. This normalization was the crucial intervention that made fair comparisons possible.

The color gradient from orange to red was implemented using Tableau's sequential color scale, with concentration values mapped to color intensity. I reversed the default scale so darker red indicates higher concentration, which aligns with cultural associations (red = strong/intense). This dual encoding—both position (bar length) and color (intensity)—makes patterns accessible through multiple channels.

Numeric labels were added by dragging the concentration measure to the Label shelf and formatting to show whole numbers. I positioned labels at the end of bars with white text on dark backgrounds and dark text on light backgrounds for maximum readability.

The sorted arrangement within each panel (highest to lowest) required setting sort order to descending by concentration value. This ensures the competitive ranking is always immediately visible—the strongest option is always at the top.

**Why this solution works:**

The redesign succeeds because it removes cognitive barriers between viewers and insights. The original table required mental calculation (180mg ÷ 30ml vs 33mg ÷ 25ml = ?), systematic scanning, and working memory. The new visualization makes these comparisons pre-attentive—you can see that Pret's deep red bar dominates before consciously processing the information.

For the target audience (coffee consumers making purchasing decisions), this provides actionable intelligence. Standing in a coffee shop deciding where to get maximum caffeine? Pret espresso. Want consistency? Starbucks. Prefer milk-based drinks? Costa cappuccino. These insights emerge instantly rather than requiring analysis.

**Reflection on the process:**

The most valuable lesson was understanding that user feedback reveals assumptions designers don't know they're making. I thought visual bar comparison would be sufficient, but users wanted numeric precision. I thought color was optional decoration, but users saw it as essential for distinguishing similar values. Testing with real people exposed these blind spots.

The critique method was equally instructive. Few's framework forced me to identify the specific failure mode (poor perceptibility due to table format) rather than just sensing something was wrong. This precision made the redesign strategy clear—I needed visual encoding and normalized metrics, not just a prettier table.

If I were to iterate further, I'd add a reference line showing average caffeine intake recommendations and possibly experiment with small multiple layouts showing each chain's full portfolio. I'd also love to test with non-technical users since both my interviewees had engineering backgrounds—would the mg per 100ml metric confuse a general audience?

The biggest challenge was balancing completeness with simplicity. I wanted to show concentration, total caffeine, volume, health context, price comparisons—but cramming everything in would recreate the original table's problems. Choosing to focus solely on concentration (the key missing metric) made the visualization more powerful by doing one thing extremely well.

## References

- Original visualization source: [[Original Visualization](https://media.product.which.co.uk/prod/images/original/d909deb408a4-935-caffeine-graphic-for-glide.png)]
- Data: Coffee caffeine content from [[original data source](https://data.world/makeovermonday/2023w9)]
- Stephen Few's Data Visualization Effectiveness Profile methodology
- MakeoverMonday challenge series: https://makeovermonday.co.uk/
- Berinato, Scott. "Good Charts: The HBR Guide to Making Smarter, More Persuasive Data Visualizations"

## AI acknowledgements

I used Gemini to support several aspects of this assignment:
- Generating the initial wireframe sketch visualization using Python/Matplotlib
- Brainstorming alternative visualization approaches (slope charts, scatter plots, heatmaps)
- Drafting portions of this portfolio narrative

All critique assessments, design decisions, user interviews, and final Tableau implementation were my own work. The AI served as a brainstorming partner and technical assistant, but all analytical judgments and creative choices came from my evaluation of the data and user feedback.
