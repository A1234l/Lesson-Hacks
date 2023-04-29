<title>
4/26 Lesson: Frontend and backend development
</title>

<table id="table" style="width: 100%;">
    <tr>
        <th>Year</th>
        <th>Month</th>
        <th>Day</th>
        <th>Cycle</th>
        <th>Trend</th>
    </tr>
</table>

<script>
const url = 'https://daily-atmosphere-carbon-dioxide-concentration.p.rapidapi.com/api/co2-api';
const options = {
	method: 'GET',
	headers: {
		'content-type': 'application/octet-stream',
		'X-RapidAPI-Key': '554c89336amsh69cd248886ad9ecp1390b5jsn24d7469d6aa0',
		'X-RapidAPI-Host': 'daily-atmosphere-carbon-dioxide-concentration.p.rapidapi.com'
	}
};

// try {
// 	const response = await fetch(url, options);
// 	const result = await response.text();
// 	console.log(result);
// } catch (error) {
// 	console.error(error);
// }

fetch(url, options)
  // response is a RESTful "promise" on any successful fetch
  .then(response => {
    // check for response errors
    if (response.status !== 200) {
        const errorMsg = 'Database read error: ' + response.status;
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
    for (let i = 0; i < 10; i++) {
      const row = data[i];
      console.log(row);
      add_row(row);
      }
    })
})

  function add_row(data) {
    const tr = document.createElement("tr");
    const year = document.createElement("td");
    const month = document.createElement("td");
    const day = document.createElement("td");
    const cycle = document.createElement("td");
    const trend = document.createElement("td");
  
    // obtain data that is specific to the API
    year.innerHTML = data.year; 
    month.innerHTML = data.month;
    day.innerHTML = data.day; 
    cycle.innerHTML = data.cycle; 
    trend.innerHTML = data.trend; 

    // add HTML to container
    tr.appendChild(year);
    tr.appendChild(month);
    tr.appendChild(day);
    tr.appendChild(cycle);
    tr.appendChild(trend);

    resultContainer.appendChild(tr);
  }
</script>