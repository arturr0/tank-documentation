# Neural Network Tank Battle - Educational Application

## Overview
Neural Network Tank Battle is an interactive educational app demonstrating supervised neural network training for physics prediction. Students learn to predict projectile outcomes via gameplay and real-time visualization.

**Key Features**
- Real-time multiplayer with WebSocket synchronization
- Physics-based projectile simulation (gravity, wind, air friction)
- Interactive neural network visualization
- Adjustable learning parameters
- Performance metrics and loss tracking

---

## User Story
**As a** student,  
**I want** to interact with a tank battle game that predicts projectile outcomes using a neural network,  
**So that** I can learn supervised learning, physics principles, and experiment with network parameters.

**Acceptance Criteria**
- Adjust learning rate and error thresholds in real time  
- Observe predictions vs actual outcomes  
- Visualize network architecture, weights, and activations  
- Multiplayer comparison for collaborative learning  
- Display performance metrics and historical loss  
- Export training data for further analysis

**Scenario:** Student sets a shot angle, observes predicted landing, fires the shot, sees actual landing, network updates weights, and adjusts parameters to improve predictions.

---

## Learning Objectives
- Supervised learning from labeled data (angle → landing)  
- Loss minimization and error correction  
- Physics integration with neural networks  
- Network architecture, optimization, and experimentation

---

## Technical Architecture

| Component         | Technology                     | Purpose                                 |
|-------------------|--------------------------------|-----------------------------------------|
| Server            | Node.js + Express + Socket.IO  | Multiplayer synchronization             |
| Client Rendering  | p5.js                          | Game visualization and UI               |
| Physics Engine    | Matter.js                      | Realistic physics simulation            |
| Data Visualization| Chart.js                       | Loss and performance metrics            |

**Neural Network**
```javascript
let mdl = {inputSize:1, hidden1Size:16, hidden2Size:16, outputSize:1,
W1:[], B1:[], W2:[], B2:[], W3:[], B3:0,
momentumW1:[], momentumW2:[], momentumW3:[],
momentumB1:[], momentumB2:[], momentumB3:0};
```

**Features**
- Real-time WebSocket communication  
- Physics simulation  
- Dynamic visualization  
- Interactive parameters

---

## Learning Progression
1. **Observation**: Visual network, weight and activation tracking, loss monitoring  
2. **Experimentation**: Adjust learning rate/error threshold, real-time updates  
3. **Prediction**: Compare predicted vs actual, historical loss, performance metrics  
4. **Application**: Modular network, export data, real-world physics constants

---

## Classroom Activities

**Parameter Optimization**
```javascript
let learningRate = 0.01;
let distanceError = 10;
```

**Physics Prediction Challenge**
```javascript
function simulateLanding(angle, shooter){
  let x=shooter.tower.x+cos(angle)*40;
  let y=shooter.tower.y+sin(angle)*40;
  let vx=cos(angle)*speed, vy=sin(angle)*speed;
  while(y<height-groundHeight){
    vx+=(-airFriction*vx+wind);
    vy+=(-airFriction*vy+gravity);
    x+=vx; y+=vy;
  }
  return x;
}
```

**Network Exploration**
- Modular structure, real-time visualization, performance metrics

---

## Technical Implementation

**Training**
```javascript
function train(){
  let angle=(startAngle+direction*progress*fullRotation)%TWO_PI;
  let landingX=simulateLanding(angle, shooter);
  let error=(landingX-target.tower.x)/width;
  backward([angle], error); updateVisualization();
}
```

**Visualization**
```javascript
function drawNeuralConnection(ctx, fromNode, toNode, weight){
  const color=weight>0?`rgba(0,200,0,${alpha})`:`rgba(200,0,0,${alpha})`;
  ctx.strokeStyle=color; ctx.lineWidth=Math.max(0.3,Math.min(3,Math.abs(weight)));
  ctx.stroke();
}
```

**Multiplayer Sync**
```javascript
socket.on('playerUpdate', d=>updateRemoteNetwork(d.player,d.angle,d.timestamp));
socket.on('roomMessage', d=>wind=d.wind);
```

---

## Assessment
- Formative: prediction accuracy, parameter optimization, error analysis  
- Summative: network design, physics projects, performance optimization

---

## Educational Dashboard
```javascript
function updateInfoPanel(){
  const info=`<strong>Player ${player}</strong><br>
  Wind: ${wind.toFixed(5)}<br>
  Distance: ${distance.toFixed(0)}<br>
  Training Samples: ${lossHistory.length}<br>
  Last Loss: ${lossHistory.length>0?lossHistory[lossHistory.length-1].toFixed(4):'N/A'}`;
  document.getElementById('infoPanel').innerHTML=info;
}
```
**Controls**: toggle weights, adjust scale, filter by activation, compare layers

---

## Extension Activities
- Transfer learning  
- Architecture comparison  
- Regularization techniques  
- Cross-disciplinary applications

---

## Implementation Guide

**Setup**
```bash
npm install express socket.io
# Load p5.js, Matter.js, Chart.js via CDN
```

**Classroom Deployment**
- Local network, pre-configured scenarios, student progress tracking

**Lesson Resources**
- Modules: Neural Networks, Projectile Motion, Gradient Descent  
- Assessment: Accuracy tracking, efficiency metrics, comparative analysis

---

## Conclusion
Neural Network Tank Battle merges technical sophistication and pedagogy, enabling students to experiment with neural networks in a meaningful context. Real-time visualization and interactive controls make AI and physics concepts accessible, engaging, and educational.
