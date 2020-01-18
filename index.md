<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Car Gifs</title>
</head>

<body>

    <button data-car="Ferrari" data-state="still" class="gif">Ferrari</button>
    <button data-car="Lamorghini" data-state="still" class="gif">Lamorghini</button>
    <button data-car="McLaren" data-state="still" class="gif">McLaren</button>
    <button data-car="Tesla" data-state="still" class="gif">Tesla</button>
    <button data-car="Porsche" data-state="still" class="gif">Porsche</button>

    <div id="gifs-appear-here">
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
    <script type="text/javascript">
        // Adding click event listen listener to all buttons
        $("button").on("click", function () {
            // Grabbing and storing the data-car property value from the button
            var car = $(this).attr("data-car");
            // Constructing a queryURL using the car name
            var queryURL = "https://api.giphy.com/v1/gifs/search?q=" +
                car + "&api_key=w2YGaDFcnQzuS78oL6oA8VjOjCDesJv7";
            // Performing an AJAX request with the queryURL
            $.ajax({
                url: queryURL,
                method: "GET"
            })
                // After data comes back from the request
                .then(function (response) {
                    console.log(queryURL);
                    console.log(response);
                    // storing the data from the AJAX request in the results variable
                    var results = response.data;
                    // Looping through each result item
                    for (var i = 0; i < results.length; i++) {
                        // Creating and storing a div tag
                        var carDiv = $("<div>");
                        // Creating a paragraph tag with the result item's rating
                        var p = $("<p>").text("Rating: " + results[i].rating);
                        // Creating and storing an image tag
                        var carImage = $("<img>");
                        // Setting the src attribute of the image to a property pulled off the result item
                        carImage.attr("src", results[i].images.fixed_height.url);
                        // Appending the paragraph and image tag to the carDiv
                        carDiv.append(p);
                        carDiv.append(carImage);
                        // Prependng the carDiv to the HTML page in the "#gifs-appear-here" div
                        $("#gifs-appear-here").prepend(carDiv);
                    }
                });

            var state = $(this).attr("data-state");

            if (state === "still") {
                var animateVal = $(this).attr("data-animate");
                $(this).attr("src", animateVal);
                $(this).attr("data-state", "animate");
            } else {
                var stillVal = $(this).attr("data-still");
                $(this).attr("src", stillVal);
                $(this).attr("data-state", "still");
            }

        });
    </script>
</body>

</html>
</body>

</html>
