---
toc: true
layout: post
description: JavaScript Exit Ticket
categories: [notes]
image: images/primitivess.jpg
title: JavaScript Exit Ticket 
---

<body>
    <table>
        <thead>
        <tr>
          <th>Name</th>
          <th>College</th>
          <th>Team?</th>
        </tr>
        </thead>
        <tbody id="result">
          <!-- generated rows -->
        </tbody>
      </table>

      <!-- Script is layed out in a sequence (no function) and will execute when page is loaded -->
      <script>
        // prepare HTML result container for new output
        const resultContainer = document.getElementById("result");
      
        // prepare fetch options
        const url = "https://localhost:8032/api/students/";
      
        const options = {
          method: 'GET',
          <!-- headers: {
              'X-RapidAPI-Key': '9e4650470emshc2461cc01c07b29p18b9b5jsnfa759ab87fca',
              'X-RapidAPI-Host': 'billboard3.p.rapidapi.com'
          } -->
        };
      
        // fetch the API
        fetch(url, options)
          // response is a RESTful "promise" on any successful fetch
          .then(response => {
            // check for response errors
            if (response.status !== 200) {
                const errorMsg = 'Database response error: ' + response.status;
                console.log(errorMsg);
                const tr = document.createElement("tr");
                const td = document.createElement("td");
                td.innerHTML = errorMsg;
                tr.appendChild(td);
                resultContainer.appendChild(tr);
                return;
            }
            // valid response will have json data
            response.json().then(data => {
                console.log(data);
      
                // Country data
                for (const row of data) {
                  console.log(row);
      
                  // tr for each row
                  const tr = document.createElement("tr");
                  // td for each column
                  const name = document.createElement("td");
                  const college = document.createElement("td");
                  const team = document.createElement("td");
      
                  // data is specific to the API
                  name.innerHTML = row.name;
                  college.innerHTML = row.college; 
                  team.innerHTML = row.team; 
      
                  // this build td's into tr
                  tr.appendChild(name);
                  tr.appendChild(college);
                  tr.appendChild(team);
      
                  // add HTML to container
                  resultContainer.appendChild(tr);
                }
            })
        })
        // catch fetch errors (ie ACCESS to server blocked)
        .catch(err => {
          console.error(err);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = err;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
        });
      </script>
</body>
