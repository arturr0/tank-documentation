# Neural Network Tank Battle - Educational Application

## Overview
Neural Network Tank Battle is an interactive educational application that demonstrates supervised neural network training applied to physics prediction problems. Students learn how neural networks can predict physical outcomes through experiential gameplay and real-time visualization.

**Key Features**
- Real-time multiplayer gameplay with WebSocket synchronization
- Physics-based projectile simulation (gravity, wind, air friction)
- Interactive neural network visualization and weight monitoring
- Adjustable learning parameters for experimentation
- Performance metrics and loss tracking for educational feedback

---

## Learning Objectives
Students gain hands-on experience with:
- Supervised learning from labeled data (angle → landing position)
- Loss minimization and error correction
- Integration of physics concepts into neural networks
- Neural network architecture, optimization, and experimentation

---

## Technical Architecture

### System Components
| Component         | Technology                     | Purpose                                 |
|-------------------|--------------------------------|-----------------------------------------|
| Server            | Node.js + Express + Socket.IO  | Real-time multiplayer synchronization   |
| Client Rendering  | p5.js                          | Game visualization and UI               |
| Physics Engine    | Matter.js                      | Realistic physics simulation            |
| Data Visualization| Chart.js                       | Loss function and performance metrics   |

### Neural Network Implementation
```javascript
// Network Architecture (1-16-16-1)
let mdl = {
  inputSize: 1, hidden1Size: 16, hidden2Size: 16, outputSize: 1,
  W1: [], B1: [], W2: [], B2: [], W3: [], B3: 0,
  momentumW1: [], momentumW2: [], momentumW3: [],
  momentumB1: [], momentumB2: [], momentumB3: 0
};
```

**Technical Features**
- Real-time WebSocket communication
- Physics-based projectile simulation
- Dynamic neural network visualization
- Interactive parameter adjustment

---

## Learning Progression

### Phase 1: Observation & Discovery
- Visual network architecture display
- Real-time weight and activation visualization
- Loss function tracking

### Phase 2: Interaction & Experimentation
- Interactive learning rate and error threshold controls
- Real-time parameter updates

### Phase 3: Prediction & Analysis
- Compare predicted vs actual outcomes
- Historical loss tracking
- Performance metrics visualization

### Phase 4: Application & Extension
- Modular network architecture for experimentation
- Exportable training data
- Physics constants reflecting real-world values

---

## Classroom Activities

### Parameter Optimization Experiment
*Goal: Understand gradient descent and learning rates*
```javascript
let learningRate = 0.01;
let distanceError = 10;
```

### Physics Prediction Challenge
*Goal: Connect models to physical outcomes*
```javascript
function simulateLanding(angle, shooter) {
  let x = shooter.tower.x + cos(angle) * 40;
  let y = shooter.tower.y + sin(angle) * 40;
  let vx = cos(angle) * speed;
  let vy = sin(angle) * speed;
  const windEffect = wind;

  while (y < height - groundHeight) {
    vx += (-airFriction * vx + windEffect);
    vy += (-airFriction * vy + gravity);
    x += vx; y += vy;
  }
  return x;
}
```

### Network Architecture Exploration
- Modular network structure allows layer experimentation
- Real-time visualization shows data flow
- Performance metrics support analysis

---

## Technical Implementation

### Neural Network Training
```javascript
function train() {
  let angle = (startAngle + direction * progress * fullRotation) % TWO_PI;
  let landingX = simulateLanding(angle, shooter);
  let error = (landingX - target.tower.x) / width;
  backward([angle], error);
  updateVisualization();
}
```

### Real-time Visualization
```javascript
function drawNeuralConnection(ctx, fromNode, toNode, weight, container) {
  const color = weight > 0 ? `rgba(0, 200, 0, ${alpha})` : `rgba(200, 0, 0, ${alpha})`;
  const lineWidth = Math.max(0.3, Math.min(3, Math.abs(weight)));
  ctx.strokeStyle = color;
  ctx.lineWidth = lineWidth;
  ctx.stroke();
}
```

### Multiplayer Synchronization
```javascript
socket.on('playerUpdate', (data) => updateRemoteNetwork(data.player, data.angle, data.timestamp));
socket.on('roomMessage', (data) => wind = data.wind);
```

---

## Assessment and Evaluation

**Formative Assessment**
- Prediction accuracy challenges
- Parameter optimization tasks
- Error analysis exercises

**Summative Assessment**
- Network architecture design
- Physics integration projects
- Performance optimization challenges

---

## Educational Dashboard
```javascript
function updateInfoPanel() {
  const info = `
    <strong>Player ${player}</strong><br>
    Wind: ${wind.toFixed(5)}<br>
    Distance: ${distance.toFixed(0)}<br>
    Training Samples: ${lossHistory.length}<br>
    Last Loss: ${lossHistory.length > 0 ? lossHistory[lossHistory.length - 1].toFixed(4) : 'N/A'}
  `;
  document.getElementById('infoPanel').innerHTML = info;
}
```

**Controls**
- Toggle weight visibility
- Adjust visualization scale
- Filter by activation strength
- Compare network layers

---

## Extension Activities
- Transfer learning challenges
- Architecture comparison studies
- Regularization techniques (dropout, weight decay)
- Cross-disciplinary applications: mathematics, computer science, scientific method

---

## Implementation Guide for Educators

### Setup Instructions
```bash
npm install express socket.io
# Client-side libraries: p5.js, Matter.js, Chart.js (via CDN)
```

### Classroom Deployment
- Local network deployment for optimal performance
- Pre-configured learning scenarios
- Student progress tracking system

### Lesson Planning Resources
- Pre-built modules: Neural Networks, Projectile Motion, Gradient Descent
- Assessment tools: Accuracy tracking, efficiency metrics, comparative analysis

---

## Conclusion
Neural Network Tank Battle combines technical sophistication with pedagogy, allowing students to experiment with neural networks in a meaningful context. Real-time visualization and interactive controls make advanced AI and physics concepts accessible and engaging, supporting both observation and advanced experimentation.
