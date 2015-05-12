angular.module('dealerApp', [])
  .controller('DealListCtrl', function ($scope, $http){
  $scope.deck =[ 
  { suit: 'Spade', value: 'A' },
  { suit: 'Spade', value: '2' },
  { suit: 'Spade', value: '3' },
  { suit: 'Spade', value: '4' },
  { suit: 'Spade', value: '5' },
  { suit: 'Spade', value: '6' },
  { suit: 'Spade', value: '7' },
  { suit: 'Spade', value: '8' },
  { suit: 'Spade', value: '9' },
  { suit: 'Spade', value: '10' },
  { suit: 'Spade', value: 'J' },
  { suit: 'Spade', value: 'Q' },
  { suit: 'Spade', value: 'K' },
  { suit: 'Diamond', value: 'A' },                                
  { suit: 'Diamond', value: '2' },
  { suit: 'Diamond', value: '3' },
  { suit: 'Diamond', value: '4' },
  { suit: 'Diamond', value: '5' },
  { suit: 'Diamond', value: '6' },
  { suit: 'Diamond', value: '7' },
  { suit: 'Diamond', value: '8' },
  { suit: 'Diamond', value: '9' },
  { suit: 'Diamond', value: '10' },
  { suit: 'Diamond', value: 'J' },
  { suit: 'Diamond', value: 'Q' },
  { suit: 'Diamond', value: 'K' },
  { suit: 'Heart', value: 'A' },                                                     
  { suit: 'Heart', value: '2' },                                  
  { suit: 'Heart', value: '3' },                                  
  { suit: 'Heart', value: '4' },                                  
  { suit: 'Heart', value: '5' },                                  
  { suit: 'Heart', value: '6' },                                  
  { suit: 'Heart', value: '7' },                                  
  { suit: 'Heart', value: '8' },                                  
  { suit: 'Heart', value: '9' },                                  
  { suit: 'Heart', value: '10' },                                 
  { suit: 'Heart', value: 'J' },                                  
  { suit: 'Heart', value: 'Q' },                                  
  { suit: 'Heart', value: 'K' },                                   
  { suit: 'Club', value: 'A' },
  { suit: 'Club', value: '2' },
  { suit: 'Club', value: '3' },
  { suit: 'Club', value: '4' },
  { suit: 'Club', value: '5' },
  { suit: 'Club', value: '6' },
  { suit: 'Club', value: '7' },
  { suit: 'Club', value: '8' },
  { suit: 'Club', value: '9' },
  { suit: 'Club', value: '10' },
  { suit: 'Club', value: 'J' },
  { suit: 'Club', value: 'Q' },
  { suit: 'Club', value: 'K' }];

  $scope.count = "Initial";
  $scope.current_prct = 100;
  $scope.average = "NA";

  $scope.prev_seq_num = 0;

  $scope.deck.getCards = function(item, event) {
     var responsePromise = $http.get("http://localhost:3000/decks/current_deck");

	responsePromise.success(function(data, status, headers, config) {

          $scope.count = Number(data["count"]);
          $scope.current_prct = Number(data["totals"]);
          $scope.average = data["avg"];
          for(var i=0; i<= data["items"].length-1; i++)
          {
            $scope.deck[i] =  data["items"][i];
          }
	});
	responsePromise.error(function(data, status, headers, config) {
	    alert("AJAX failed!");
	});
    }

  $scope.deck.getPrevious = function(item, event) {
    var responsePromise = $http.get("http://localhost:3000/decks/historical/" + $scope.prev_seq_num);

    responsePromise.success(function(data, status, headers, config) {
      if(data.hasOwnProperty("items"))
      {
	$scope.count = Number(data["count"]);
	$scope.current_prct = Number(data["totals"]);
	for(var i=0; i<= data["items"].length-1; i++)
	{
	  $scope.deck[i] =  data["items"][i];
	}
      }
      else
      {
        alert("That sequence number does not correspondond to an existing configuration");
      }
    });
    responsePromise.error(function(data, status, headers, config) {
	alert("AJAX failed!");
    });
  }

  $scope.deck.shuffle_and_deal = function(item, event) {

        var responsePromise = $http.get("http://localhost:3000/decks");

	responsePromise.success(function(data, status, headers, config) {
          $scope.count = Number(data["count"]);
          $scope.current_prct = Number(data["totals"]);
          $scope.average = data["avg"];
          for(var i=0; i<= data["items"].length-1; i++)
          {
            $scope.deck[i] =  data["items"][i];
          }

         // $scope.highlight();
	});
	responsePromise.error(function(data, status, headers, config) {
	    alert("AJAX failed!");
	});
     
    }


  $scope.highlight_pairs = function(card_grid)
  {
    for(var i=0; i<=3; i++)
    {
      for(var j=0; j<=11; j++)
      {
	if(card_grid[i][j]["value"] === card_grid[i][j+1]["value"])
        {
          $("#card_" + ((13*i)+j)).addClass("pair");
          $("#card_" + ((13*i)+(j+1))).addClass("pair");
        }
      }
    }  
  }

  $scope.highlight_triplets = function(card_grid)
  {
    for(var i=0; i<=3; i++)
    {
      for(var j=0; j<=10; j++)
      {
	if(card_grid[i][j]["value"] === card_grid[i][j+1]["value"] && card_grid[i][j+1]["value"] === card_grid[i][j+2]["value"])
        {
          $("#card_" + ((13*i)+j)).addClass("triplet");
          $("#card_" + ((13*i)+(j+1))).addClass("triplet");
          $("#card_" + ((13*i)+(j+2))).addClass("triplet");
        }
      }
    }  
  }

  $scope.highlight = function()
  {
    var card_grid = [[],[],[],[]];
    var k=0;
    for(var i=0; i<= 3; i++)
    {
      for(var j=0; j<=12; j++)
      {
        card_grid[i][j] = $scope.deck[k];
        k++;
      }
    }
    $scope.highlight_pairs(card_grid);
    $scope.highlight_triplets(card_grid);
  }
    

})
.config(function($interpolateProvider){
    $interpolateProvider.startSymbol('{[{').endSymbol('}]}');
  })
;
