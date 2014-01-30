JitteryRatings
==============

JJ's Coffee shop Ratings for top blends

The changes are as follows:

- First we have to create an array to match the ratings to, so in app.js, right under *$scope.reviews* we'll create:

          $scope.reviewCount = [
          { "name": "After Dinner", "count": 0, "sum": 0, "average": 0},
          { "name": "Bourque Newswatch", "count": 0, "sum": 0, "average": 0},
          { "name": "CN Tower of Power", "count": 0, "sum": 0, "average": 0},
          { "name": "Connoisseur Estates", "count": 0, "sum": 0, "average": 0},
          { "name": "Columbian", "count": 0, "sum": 0, "average": 0},
          { "name": "Fordnation Blend", "count": 0, "sum": 0, "average": 0},
          { "name": "Hawaii Kona", "count": 0, "sum": 0, "average": 0},
          { "name": "House Blend", "count": 0, "sum": 0, "average": 0},
          { "name": "Italian Roast", "count": 0, "sum": 0, "average": 0},
          { "name": "Lionel Roastie", "count": 0, "sum": 0, "average": 0},
          { "name": "Mocca-Java", "count": 0, "sum": 0, "average": 0},
          { "name": "Reggae Blend", "count": 0, "sum": 0, "average": 0},
          { "name": "Ruth Roast", "count": 0, "sum": 0, "average": 0},
          { "name": "Toronto Blend", "count": 0, "sum": 0, "average": 0},
          { "name": "Tropic of Coffee", "count": 0, "sum": 0, "average": 0},
          { "name": "World Tour Blend", "count": 0, "sum": 0, "average": 0}
          ]

- Then when we get the reviews data, we'll have to start sorting it
- Right under *$scope.reviews = data* we'll add

        for (var i = 0; i < $scope.reviews.length; i++) {
          var coffeeType = $scope.reviews[i].item;
          var coffeeRating = $scope.reviews[i].rating;

- This goes through the data we just got and assigns the coffee name and its rating to a variable
- We'll then need to go through our list that we have to change up the metrics of our list
        
        for (var k = 0; k < $scope.reviewCount.length; k++) {
          if (coffeeType == $scope.reviewCount[k].name) {
            $scope.reviewCount[k].count++;
            $scope.reviewCount[k].sum += parseInt(coffeeRating);
            $scope.reviewCount[k].average = $scope.reviewCount[k].sum / $scope.reviewCount[k].count;
          };
        };

- Now we have the metrics for all our coffee yay :D
- To order this list we use the Sort Array function

        $scope.reviewCount.sort(function(a, b){
          return b.average-a.average
        })

- And to get the top 3 we'll just add the first 3 of our sorted list to a new list

        $scope.top3 = [];
          for (var i = 0; i < 3; i++) {
            $scope.top3.push($scope.reviewCount[i])
        };
