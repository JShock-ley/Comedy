\<\!DOCTYPE html\>  
\<html\>  
\<head\>  
    \<title\>Comedy Style Quiz\</title\>  
    \<script src="https://cdn.jsdelivr.net/npm/chart.js"\>\</script\>  
\</head\>  
\<body\>  
    \<h2\>Comedy Style Quiz\</h2\>  
    \<div id="quiz"\>\</div\>  
    \<button onclick="calculateScore()"\>Submit\</button\>  
    \<canvas id="resultChart" width="400" height="400"\>\</canvas\>  
      
    \<script\>  
        const questions \= \[  
            { text: "I told my wife she should embrace her mistakes. She gave me a hug.", x: \-1, y: \-1 },  
            { text: "So I walked into a coffee shop, and the barista whispered, 'The pigeons are watching.'", x: 1, y: 1 },  
            { text: "The boat was sinking... 'Bit of a rough crossing, eh?'", x: 1, y: \-1 },  
            { text: "A man steps onto an escalator, flails, and topples into oranges.", x: \-1, y: 1 },  
            { text: "So there I was, in a haunted bowling alley...", x: 2, y: 0 },  
            { text: "People say nothing is impossible, but I do nothing every day.", x: \-2, y: \-1 },  
            { text: "I dropped my sandwich. My soul left my body.", x: \-1, y: 2 }  
        \];

        const quizDiv \= document.getElementById("quiz");  
        questions.forEach((q, index) \=\> {  
            let questionHTML \= \`\<p\>${q.text}\</p\>\`;  
            for (let i \= 1; i \<= 5; i++) {  
                questionHTML \+= \`\<label\>\<input type='radio' name='q${index}' value='${i}'\> ${i}\</label\>\`;  
            }  
            quizDiv.innerHTML \+= questionHTML \+ "\<br\>";  
        });

        function calculateScore() {  
            let xScore \= 0, yScore \= 0;  
            questions.forEach((q, index) \=\> {  
                let selected \= document.querySelector(\`input\[name='q${index}'\]:checked\`);  
                if (selected) {  
                    let value \= parseInt(selected.value) \- 3;  
                    xScore \+= q.x \* value;  
                    yScore \+= q.y \* value;  
                }  
            });  
            displayChart(xScore, yScore);  
        }

        function displayChart(x, y) {  
            const ctx \= document.getElementById('resultChart').getContext('2d');  
            new Chart(ctx, {  
                type: 'scatter',  
                data: {  
                    datasets: \[{  
                        label: 'Your Comedy Style',  
                        data: \[{ x: x, y: y }\],  
                        backgroundColor: 'red',  
                        pointRadius: 10  
                    }\]  
                },  
                options: {  
                    scales: {  
                        x: { title: { display: true, text: 'Contained (-) ←→ Context (+)' }, min: \-10, max: 10 },  
                        y: { title: { display: true, text: 'Dry (-) ←→ Wet (+)' }, min: \-10, max: 10 }  
                    }  
                }  
            });  
        }  
    \</script\>  
\</body\>  
\</html\>

