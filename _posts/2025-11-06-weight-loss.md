---
layout: post
title: "A Developer's experience with weight loss injections"
categories: [personal, weight-loss]
---

This is a personal account of my experiences taking weight loss medication.
Quite a departure from my usual content.

I have no doubt that you are smart enough *not* to take medical advice from some random nerd on the internet, but let me say it anyway: none of the following is medical advice.
I want to share my experiences and perspectives in addition to a vibe-coded tool, but I'm not trying to convince you of anything.
Please don't take my word for anything health related&mdash;talk to a medical professional first!

Got it? Good.


One of my main goals from my year off was to lose weight, which had been creeping upwards (albeit *slowly*) over the years.
When I started my sabbatical in June I had reached 100kg which pushed me just over the threshold from overweight to obese.

Of course this shocked me.
Doubly so, because I didn't feel that big.
If I were to walk out of my house on any given day I would pass plenty of other folk with much larger waistlines than mine.
Living in a country 🏴󠁧󠁢󠁳󠁣󠁴󠁿 were deep frying is a religion and "juice" doesn't contain fruit, clearly gave me a false perspective.

[![Scottish food](../images/DeepFriedMarsBar.jpg)](https://en.wikipedia.org/wiki/Deep-fried_Mars_bar)
*Scottish food*

Although I didn't feel so large, I was very much aware of a number of weight related health issues dragging my quality of life downwards.
For years I had managed these issue, but I could see they weren't going to improve without losing weight.

There was a time (~10 years ago) when I was in good shape and my weight was stable.
I attributed this to running.
A 5km three times a week and the occasional 10km plus some resistance training meant I could eat more-or-less what I wanted.
The turning point was when I developed a *herniated disc*.
An hour's run would be followed by 48 hours of constant back pain.

Incidentally, a herniated disc must be the dumbest flaw in the human body.
The human spine is a miraculous thing, but the "discs" (essentially washers that separate vertebrae) are prone to (literal) bursting.
Around 50% of the population have a herniated disc by the age of 50.
Most cause no symptoms, but in some people (like myself) the bulging disc presses on a nerve, causing pain.
If there were a git repository for the human body, I would surely file a passive-aggressive issue.
I might remark on that issue how it was clearly a poor choice to install a component with 50 year life span into something expected to last at least 80 years.

Exercises recommended by a physio didn't help (they actually made it worse).
Heat packs, cold packs, ibuprofen, and massage offered only short term relief.

When I stopped running for a few days the pain became an occasional sharp piercing pain rather than a constant ache.
Not great, but bearable.

And so ended my running career.

I replaced the running with nothing at all.
Other than walking (more as my default method of transport) I didn't really exercise.
I can't attribute this entirely to the back pain.
There are several forms of exercise that don't inflame the back pain, such as swimming.
I just didn't find anything that I enjoyed doing regularly in the same way as running.

My diet is fairly healthy&mdash;for a Scot at least.
I suspected I am in the top 0.1% percentile in the country for eating vegetables (and I'm not counting potato).
My downfall is more sweet foods, which I typically indulge in my morning pastry and coffee.
The rest of the day I try to eat healthy.
I watch portion size and routinely deny myself things I would enjoy eating (trust me: if I ate all the sweet things I wanted to, my diet would be 90% cinnamon buns).

Alas, this wasn't enough to keep the weight down.
The scales don't lie, and they were telling me I was getting heaver over time, which meant I was consuming more calories than I was expending.
But how many more calories was I eating?

Turns out that is easy to calculate.
There are approximately 7,700 calories in 1kg of human fat (eww&mdash;try not to imagine 1kg of fat).
I had gained 8.5kg in 1400 days, which works out as a ~47 calorie excess per day.
Around half an apple's worth.

Half an apple?
Two or three additional mouthfuls a day is all it takes to put you on a trajectory to being overweight / obese and all the health issues that entails.
Yeah, well that was an eye opener.

If you are gaining or losing weight yourself, you might want to try this tool I vide-coded with [Toad](https://willmcgugan.github.io/categories/#toad) and Claude:

<div class="calorie-calculator">
    <h3>Excess Calorie Calculator</h3>
    
    <div class="form-group">
        <label for="startWeight">Starting Weight (kg)</label>
        <input type="number" id="startWeight" step="0.1" placeholder="e.g., 70.0">
    </div>
    
    <div class="form-group">
        <label for="endWeight">Ending Weight (kg)</label>
        <input type="number" id="endWeight" step="0.1" placeholder="e.g., 73.5">
    </div>
    
    <div class="form-group">
        <label for="startDate">Start Date</label>
        <input type="date" id="startDate">
    </div>
    
    <div class="form-group">
        <label for="endDate">End Date</label>
        <input type="date" id="endDate">
    </div>
    
    <button class="calculate-btn" onclick="calculateCalories()">Calculate</button>
    
    <div class="error" id="error"></div>
    
    <div class="results" id="results">
        <h3>Results</h3>
        <div class="result-item">
            <div class="result-label">Weight Change:</div>
            <div class="result-value" id="weightChange"></div>
        </div>
        <div class="result-item">
            <div class="result-label">Time Period:</div>
            <div class="result-value" id="timePeriod"></div>
        </div>
        <div class="result-item">
            <div class="result-label">Total Excess Calories:</div>
            <div class="result-value" id="totalCalories"></div>
        </div>
        <div class="result-item">
            <div class="result-label">Excess Calories Per Day:</div>
            <div class="result-value" id="caloriesPerDay"></div>
        </div>
    </div>
</div>

<style>
    .calorie-calculator {
        max-width: 500px;
        margin: 20px auto;
        padding: 20px;
        border: 1px solid #ddd;
        border-radius: 8px;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
        background-color: #f9f9f9;
    }
    
    .calorie-calculator h2 {
        margin-top: 0;
        color: #333;
        font-size: 1.5em;
    }
    
    .form-group {
        margin-bottom: 15px;
    }
    
    .form-group label {
        display: block;
        margin-bottom: 5px;
        font-weight: 500;
        color: #555;
    }
    
    .form-group input {
        width: 100%;
        padding: 8px;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        font-size: 14px;
    }
    
    .form-group input:focus {
        outline: none;
        border-color: #4CAF50;
    }
    
    .calculate-btn {
        width: 100%;
        padding: 10px;
        background-color: #4CAF50;
        color: white;
        border: none;
        border-radius: 4px;
        font-size: 16px;
        font-weight: 500;
        cursor: pointer;
        margin-top: 10px;
    }
    
    .calculate-btn:hover {
        background-color: #45a049;
    }
    
    .results {
        margin-top: 20px;
        padding: 15px;
        background-color: white;
        border-radius: 4px;
        border-left: 4px solid #4CAF50;
        display: none;
    }
    
    .results.show {
        display: block;
    }
    
    .results h3 {
        margin-top: 0;
        color: #333;
        font-size: 1.2em;
    }
    
    .result-item {
        margin: 10px 0;
        padding: 8px 0;
        border-bottom: 1px solid #eee;
    }
    
    .result-item:last-child {
        border-bottom: none;
    }
    
    .result-label {
        font-weight: 500;
        color: #666;
    }
    
    .result-value {
        font-size: 1.1em;
        color: #333;
        font-weight: 600;
    }
    
    .result-value.positive {
        color: #d32f2f;
    }
    
    .result-value.negative {
        color: #388e3c;
    }
    
    .error {
        color: #d32f2f;
        font-size: 14px;
        margin-top: 5px;
        display: none;
    }
    
    .error.show {
        display: block;
    }
</style>

<script>
    const CALORIES_PER_KG = 7700;

    function calculateDaysBetween(startDate, endDate) {
        const start = new Date(startDate);
        const end = new Date(endDate);
        const diffTime = end - start;
        const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
        return diffDays;
    }

    function calculateTotalExcessCalories(weightStart, weightEnd) {
        const weightChange = weightEnd - weightStart;
        return weightChange * CALORIES_PER_KG;
    }

    function showError(message) {
        const errorDiv = document.getElementById('error');
        errorDiv.textContent = message;
        errorDiv.classList.add('show');
        document.getElementById('results').classList.remove('show');
    }

    function hideError() {
        document.getElementById('error').classList.remove('show');
    }

    function calculateCalories() {
        hideError();

        // Get input values
        const startWeight = parseFloat(document.getElementById('startWeight').value);
        const endWeight = parseFloat(document.getElementById('endWeight').value);
        const startDate = document.getElementById('startDate').value;
        const endDate = document.getElementById('endDate').value;

        // Validate inputs
        if (!startWeight || !endWeight || !startDate || !endDate) {
            showError('Please fill in all fields');
            return;
        }

        if (startWeight <= 0 || endWeight <= 0) {
            showError('Weight values must be positive');
            return;
        }

        const days = calculateDaysBetween(startDate, endDate);

        if (days <= 0) {
            showError('End date must be after start date');
            return;
        }

        // Calculate results
        const weightChange = endWeight - startWeight;
        const totalExcessCalories = calculateTotalExcessCalories(startWeight, endWeight);
        const caloriesPerDay = totalExcessCalories / days;

        // Display results
        document.getElementById('weightChange').textContent = 
            `${weightChange > 0 ? '+' : ''}${weightChange.toFixed(1)} kg`;
        
        document.getElementById('timePeriod').textContent = 
            `${days} day${days !== 1 ? 's' : ''}`;
        
        const totalCaloriesElement = document.getElementById('totalCalories');
        totalCaloriesElement.textContent = 
            `${totalExcessCalories > 0 ? '+' : ''}${totalExcessCalories.toFixed(0)} kcal`;
        totalCaloriesElement.className = 'result-value ' + (totalExcessCalories > 0 ? 'positive' : 'negative');
        
        const caloriesPerDayElement = document.getElementById('caloriesPerDay');
        caloriesPerDayElement.textContent = 
            `${caloriesPerDay > 0 ? '+' : ''}${caloriesPerDay.toFixed(0)} kcal/day`;
        caloriesPerDayElement.className = 'result-value ' + (caloriesPerDay > 0 ? 'positive' : 'negative');

        // Show results
        document.getElementById('results').classList.add('show');
    }

    // Allow Enter key to trigger calculation
    document.querySelectorAll('input').forEach(input => {
        input.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                calculateCalories();
            }
        });
    });

    // Set default dates (today and 2 months ago)
    const today = new Date();
    const twoMonthsAgo = new Date();
    twoMonthsAgo.setMonth(today.getMonth() - 2);
    
    document.getElementById('endDate').valueAsDate = today;
    document.getElementById('startDate').valueAsDate = twoMonthsAgo;
</script>


So the weight gain is no mystery&mdash;I was simply eating to excess.
The solution was also no mystery.
I would have have to stop consuming that additional 47 calories a day to stabilize my weight.
And then reduce it further to reverse the trend.

If I were to subtract *another* 47 calories in addition to the 47 excess calories, then I would lose weight at the same rate I had previously been gaining.
In other words, eating 94 calories less a day I would return to my healthy weight (~80kg) in about 9 years.

Screw that.

I have a year off to focus on my health, not 9 years.
Losing 20kg in a year would require a 422kcal deficit, on top of the 47 excess I had been eating.

That's quite doable with healthier food choices and exercise.
I could give up my morning pastry and take up swimming.
But its hard to avoid hearing about weight loss medications, and after looking into it I was tempted.
Ultimately I settled on Mounjaro as it is reported to lead to the greatest weight loss.

The medication comes in a format described as "pen".
In reality of course it is a syringe, albeit a cleverly designed one designed to deliver 4 measured doses.

I don't have a problem with needles but I was a little apprehensive about injecting myself.
I needn't have been.
The needle is tiny (less than 1cm and almost as thin as a human hair), and only needs to go just under the skin to a fat layer.
You bring it down in a stabbing motion and press a button at the top of the "pen" until it delivers the dose.

![Pulp fiction stab](../images/pulp-fiction-stab.gif)

In the first week it was immediately apparent that the medication was doing something.
It did suppress my appetite, but in those first weeks I consciously didn't eat much at all as any meal resulted in gastric symptoms.
I'll spare you the details, but that first month the weight loss was dramatic.
The second month was a little better and I could really appreciate the reduction in my appetite.

My wife and I have a running joke.
When I'm hungry I tell her "if I don't eat in the next 15 minutes I am going to *die*".
She replies "give it a try".
Well I never did give it a try until recently and it turns out she was right.
The sensation of hunger was far less urgent, and I could put it off for way more than 15 minutes.
And when I did eat, I felt like I was done after a very small portion.

Paradoxically I also found that my energy levels were positively brimming during the first two months.
From morning until evening I had loads of energy and of course I wasn't suffering from a post-lunch slump or evening sluggishness.
I was still suffering from stomach issues, but the increase in energy and clear weight-loss felt like fair compensation.

The stomach issues improved somewhat but were relatively constant throughout the whole experience.
Alas the high energy levels disappeared after two months or so.
The weight loss was rapid, averaging 1kg a week, which is borderline concerning.
I always ate to my appetite and intentionally chose nutritious high-energy foods, hoping to slow down the weight loss just a bit.
But I just couldn't face eating after a point.

At about 3 months or so after starting Mounjaro I started experiencing another symptom: frequent head-rushes.
I would stand up from a sitting or laying position and instantly feel woozy.
Often leaning against the wall in case I blacked out (I never did).
I would be back to normal after 30 seconds, but this occurred often enough to be a worry.

This turned out to be only indirectly related to the Mounjaro.
I had been on blood pressure medication for a couple of years, and with my blood pressure coming down naturally from the weight loss the medication was too effective.
My GP reduced the medication by half and monitored my blood pressure for another month.
The head-rushes abated and I eventually come off the blood pressure medication altogether.
What a result!

My back pain has also improved.
It hasn't gone away, but the frequency and intensity of bad-back days has reduced remarkably.
If that wasn't enough, I haven't had a single bout of [GORD](https://www.nhsinform.scot/illnesses-and-conditions/stomach-liver-and-gastrointestinal-tract/gastro-oesophageal-reflux-disease-gord/) since losing the weight.

It's now 5 months on since I started Mounjaro, and I have taken my last dose.
I lost just over 20kg which puts me in my ideal weight bracket.
It has been no cake-walk, but I consider the months-long stomach ache to be worth it for the health benefits it has delivered.
I'm looking forward to enjoying food again, but I'm highly motivated not to eat the 47 calories a day that made me obese.

Reflecting on the wider impacts of Mounjaro and similar drugs.
These must surely be the largest change to public health since anti-biotics.
Many of the conditions that kill people in their 50s onwards are made worse if not outright caused by being overweight or obese.
If everyone can get their weight under control it will dramatically reduce rates of diabetes, heart disease, stroke, and cancer.
We will all be living longer more productive lives as a result.

Let me finish by re-iterating that I'm not giving health advice.
Talk to a doctor if you are considering taking any medication, not a Python developer.