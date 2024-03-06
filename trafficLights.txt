function trafficLights(initRoad, n) {
  var timeStampRoad = [initRoad];
  initRoad = initRoad.split('');
  //first Lights
  var lightsState = initRoad.map((space, i) => {
    if (space === 'G' || space === 'R') {
      return { currentState: space, timeToChange: 5, position: i }
    }
    if (space === 'O') {
      return { currentState: space, timeToChange: 1, position: i }
    }
  }).filter(e => e ? true : false);
  for (let i = 0; i < n; i++) {
    var currentState = timeStampRoad[timeStampRoad.length - 1].split('');
    for (let j = currentState.length - 1; j > -1; j--) {
      var nLP = lightsState.findIndex(l => l.position === j);
      if (nLP > -1) {
        if (lightsState[nLP].timeToChange === 1) {
          if (lightsState[nLP].currentState === 'G') {
            console.log('test')
            lightsState[nLP].currentState = 'O';
            lightsState[nLP].timeToChange = 1;
          }else if (lightsState[nLP].currentState === 'O') {
            console.log('test3')
            lightsState[nLP].currentState = 'R';
            lightsState[nLP].timeToChange = 5
          }else if (lightsState[nLP].currentState === 'R') {
            console.log('test2')
            lightsState[nLP].currentState = 'G';
            lightsState[nLP].timeToChange = 5
          }
          console.log(lightsState)
          currentState[j] = currentState[j] === 'C' ? 'C' : lightsState[nLP].currentState; 
        } else { 
          lightsState[nLP].timeToChange-- ;
        }
      }

      //thenCars
      if (currentState[j] === 'C') {
        if (!currentState[j + 1]) { 
          currentState[j] = nLP > -1 ? lightsState[nLP].currentState : '.';
        } else if (
          (currentState[j + 1] === '.') || 
          (currentState[j + 1] === 'G' && !currentState[j + 2]) || 
          (currentState[j + 1] === 'G' && currentState[j + 2] === '.')
        ) {
          currentState[j + 1] = 'C';
          currentState[j] = nLP > -1 ? lightsState[nLP].currentState : '.';
        }
      }
    }

    timeStampRoad.push(currentState.join(''));
  }

  return timeStampRoad;
}

