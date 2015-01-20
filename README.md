<!DOCTYPE html>
<html>
<head>
    <!--Load the AJAX API-->
    <script type="text/javascript" src="https://www.google.com/jsapi"></script>
    <script type="text/javascript">
    // Load the Visualization API and the core charts package.
    google.load('visualization', '1.0', {
        'packages': ['corechart']
    });

    // Set a callback to run when the Google Visualization API is fully loaded.
    google.setOnLoadCallback(getData);

    function getData() {
        // this is the key for the spreadhseet with your data in it, you can copy this from the URL for the sheet
        var key = "1gIytFC4RV-FnRabk3h52vYiTd5tppKY1ac75uisuTqc";
        // this is the range in the sheet to find the data
        var range = "A1:B50";
        // get the date from the range specified
        var query = new google.visualization.Query('https://docs.google.com/spreadsheet/ccc?key=' + key + '&usp=sharing&range=' + range);
        // Send the query with a callback function, to be executed when the data is reeady
        query.send(drawChart);
    }


    // Callback that creates and populates a data table,
    // instantiates the line chart, passes in the data and
    // draws it.
    function drawChart(response) {

        // standard bit of code in case we are offline or you deleted the google sheet or something like that
        if (response.isError()) {
            console.log('Error in query: ' + response.getMessage() + ' ' + response.getDetailedMessage());
            return;
        }

        // dig out the data from the response to the query 
        var data = response.getDataTable();
        // there are squillions of cool options for your charts, shove them into this JSON object
        // read more https://developers.google.com/chart/interactive/docs/gallery/linechart
        var options = {
            'title': 'Tweet Volume By Minute (15:00 - 15:49, Decemeber 1st)',
            'width': 1000,
            'height': 400,
            'legend': { position: 'in'}
        };

        // Instantiate and draw our line chart, passing in the options JSON object.
        var chart = new google.visualization.LineChart(document.getElementById('chart_div'));
        chart.draw(data, options);
    }
    </script>
</head>
 
<body>
    <!--Div that will hold the pie chart-->
    <div id="chart_div"></div>
</body>
 
</html>
