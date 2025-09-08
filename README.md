# Neural Network Tank Battle - Educational Application

## Project Links
- **Repository:** [GitHub Repo](https://github.com/arturr0/ai-tillery)
- **Live Demo:** [Website Demo](https://tank-rooms.onrender.com/)

## Overview
Neural Network Tank Battle is an interactive educational app demonstrating supervised neural network training for physics prediction. Students learn to predict projectile outcomes via gameplay and real-time visualization.

**Key Features**
- Real-time multiplayer with WebSocket synchronization  
- Physics-based projectile simulation (gravity, wind, air friction)  
- Interactive neural network visualization  
- Adjustable learning parameters (architecture + training)  
- Performance metrics and loss tracking  

---

## User Story
**As a** student,  
**I want** to interact with a tank battle game that predicts projectile outcomes using a neural network,  
**So that** I can learn supervised learning, physics principles, and experiment with network parameters.

**Acceptance Criteria**
- Create/join room on root page, wait for second player  
- Customize neural network (hidden layers, nodes, activation, bias) before battle  
- Both confirm readiness (time limit for design phase)  
- During battle adjust learning rate, max error (shooting threshold), and other parameters  
- Observe predictions vs actual outcomes  
- Visualize network structure and performance metrics  
- Export training data for further study  

**Scenario:**  
Two players enter a room → each configures their NN → time-limited design phase ends when both are ready → training begins → during combat players tweak training parameters while network learns in real time.

---

## Learning Objectives
- Supervised learning from labeled data (angle → landing)  
- Loss minimization and error correction  
- Physics + neural network integration  
- Neural architecture design and optimization  

---

## Technical Architecture
| Component         | Technology                     | Purpose                                 |
|-------------------|--------------------------------|-----------------------------------------|
| Server            | Node.js + Express + Socket.IO  | Multiplayer synchronization             |
| Client Rendering  | p5.js                          | Game visualization and UI               |
| Physics Engine    | Matter.js                      | Projectile motion simulation            |
| Data Visualization| Chart.js                       | Loss/performance metrics                |

**Neural Network Example**
```javascript
let mdl={inputSize:1, hidden1Size:16, hidden2Size:16, outputSize:1,
W1:[],B1:[],W2:[],B2:[],W3:[],B3:0,
momentumW1:[],momentumW2:[],momentumW3:[],
momentumB1:[],momentumB2:[],momentumB3:0};
```

---

## Learning Progression
1. **Observation**: Visualize network + loss function  
2. **Experimentation**: Adjust layers/nodes, activation, biases  
3. **Prediction**: Compare predicted vs actual outcomes  
4. **Application**: Export data, real-world parameterization  

---

## Classroom Activities
**Parameter Optimization**
```javascript
let learningRate=0.01;
let distanceError=10;
```

**Physics Prediction Challenge**
```javascript
function simulateLanding(angle, shooter){
  let x=shooter.tower.x+cos(angle)*40, y=shooter.tower.y+sin(angle)*40;
  let vx=cos(angle)*speed, vy=sin(angle)*speed;
  while(y<height-groundHeight){
    vx+=(-airFriction*vx+wind);
    vy+=(-airFriction*vy+gravity);
    x+=vx; y+=vy;
  }
  return x;
}
```

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
function drawNeuralConnection(ctx,from,to,weight){
  const c=weight>0?`rgba(0,200,0,${alpha})`:`rgba(200,0,0,${alpha})`;
  ctx.strokeStyle=c; ctx.lineWidth=Math.max(0.3,Math.min(3,Math.abs(weight))); ctx.stroke();
}
```

**Multiplayer**
```javascript
socket.on('playerUpdate',d=>updateRemoteNetwork(d.player,d.angle,d.timestamp));
socket.on('roomMessage',d=>wind=d.wind);
```

---

## Assessment
- **Formative**: prediction accuracy, error analysis, parameter exploration  
- **Summative**: network design, physics integration projects, optimization tasks  

---

## Dashboard & Controls
```javascript
function updateInfoPanel(){
  document.getElementById('infoPanel').innerHTML=`
    <strong>Player ${player}</strong><br>
    Wind: ${wind.toFixed(5)}<br>
    Distance: ${distance.toFixed(0)}<br>
    Training Samples: ${lossHistory.length}<br>
    Last Loss: ${lossHistory.at(-1)?.toFixed(4)??'N/A'}`;
}
```
- Toggle weights, adjust visualization scale  
- Filter activations, compare layers  
- Adjust learning rate, max error, biases during combat  

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

**Deployment**
- Local network with pre-configured scenarios  
- Time-limited NN design phase  
- Track student progress  

---

## Conclusion
Neural Network Tank Battle combines physics, AI, and gameplay for experiential learning. Students design networks, tune training, and engage in real-time battles, making advanced AI and physics concepts engaging and hands-on.
