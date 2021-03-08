# machine-learning-trigiang

let model;
//to identify the letter when pressed in an area
let targetLable = 'C';
let trainingData = [];
//to set the state as collection when clicking in the areas to name them
let state = 'collection'
function setup() {
        createCanvas(400, 400);
 let options = {
   inputs: ['x', 'y'],
   outputs: ['label'],
   task: 'classification',
   debug:'true'
 };
//neural network library
  model = ml5.neuralNetwork(options);
}
//to have the machine start training after collecting the data
function keyPressed(){

if (key=='t'){
  state = 'training '
  console.log('starting training');
  model.normalizeData();
//number of times machine goes through data
  let options={
    epochs:200
  }
//log the training data
  console.log(trainingData)
  model.train(options, finishTraining);
} else {
//have all labled area to be Upper case letter
  targetLable = key.toUpperCase();
  }
}
//calculate the error and improvement over time of learning process
function whileTraining(epochs, loss){
  console.log(epoch);
}
//after training, the machine is able to begin identify 
function finishTraining(){
  console.log ('finished training.');
  state = 'prediction'
}

function mousePressed(){

let inputs = {
  x: mouseX,
  y: mouseY
}
if (state=='collection'){

let target = {
  lable: targetLable
}

//the style of the labels
model.addData(inputs, target);
  stroke (0);
  noFill();
  ellipse(mouseX, mouseY, 24);
  fill(0);
  noStroke();
  textAlign(CENTER, CENTER);
  text(targetLable, mouseX, mouseY);
} else if (state =='prediction'){
  model.classify(inputs, gotResults);
}

}
//identifying the labels and giving it a percentage of error
function gotResults(error, results){
  if (error){
    console.error(error);
    return;
}
//labeling the selected area and determining the correct label
  console.log(results);
  stroke (0);
  fill(0,0,255,100);
  ellipse(mouseX, mouseY, 24);
  fill(0);
  noStroke();
  textAlign(CENTER, CENTER);
  text(results[0].label, mouseX, mouseY);
}
