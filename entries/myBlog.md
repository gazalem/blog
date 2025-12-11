---
title: "My Blog"
date: 2025-12-11
tags: [blog, articles]
author: Alan
---
# My Blog

This is a test

```javascript
let result = "";

function compareResponses(formData, rightResponses) {
    let differences = [];

    const userAnswers = {};
    formData.TicketData.Attributes.forEach(attr => {
        // The correct answer for the question determines if we should treat the value as an array
        if (Array.isArray(rightResponses.Response[attr.Name])) {
            // The value is a string like "55237, 55235, 55232"
            // We split it into an array and sort it for comparison.
            userAnswers[attr.Name] = attr.Value.split(', ').sort();
        } else {
            userAnswers[attr.Name] = attr.Value;
        }
    });

    for (let key in rightResponses.Response) {
        if (Object.prototype.hasOwnProperty.call(rightResponses.Response, key)) {
            let userAnswer = userAnswers[key];
            let rightResponse = rightResponses.Response[key];

            if (Array.isArray(rightResponse)) {
                // Also sort the correct answer array to ensure a match.
                let rightResponseSorted = [...rightResponse].sort();
                if (JSON.stringify(userAnswer) !== JSON.stringify(rightResponseSorted)) {
                    differences.push(`<br><span>Question ${key.substring(27)}. Must be answered correctly.</span>`);
                }
            } else if (userAnswer !== rightResponse) {
              differences.push(`<br><span>Question ${key.substring(27)}. Must be answered correctly.</span>`);
            }
        }
    }

    if (differences.length === 0) {
        result = "<strong>You passed the Essential Training Quiz.</strong><br>";
    } else {
        result = `<br><strong>Please review the following answers:</strong><br>`;
        result += differences.join("\n");
    }
}

compareResponses(FlowInput, quizResponses);




let result = `<br><br><span>RETAKE HERE: <a href="https://td.byui.edu/TDClient/78/Portal/KB/ArticleDet?ID=10103">FACTA Essential Training Quiz<\a><\span>`;
```
