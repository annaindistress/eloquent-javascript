# Project: A Robot

## Measuring a robot

It’s hard to objectively compare robots by just letting them solve a few scenarios. Maybe one robot just happened to get easier tasks or the kind of tasks that it is good at, whereas the other didn’t.

Write a function `compareRobots` that takes two robots (and their starting memory). It should generate 100 tasks and let each of the robots solve each of these tasks. When done, it should output the average number of steps each robot took per task.

For the sake of fairness, make sure you give each task to both robots, rather than generating different tasks per robot.

### Solution

```js
function countSteps (state, robot, memory) {
  for (let step = 0;; step++) {
    if (state.parcels.length === 0) return step;
    let action = robot(state, memory);
    state = state.move(action.direction);
    memory = action.memory
  }
};

function compareRobots (robot1, memory1, robot2, memory2) {
  let steps1 = 0, steps2 = 0;
  for (let i = 0; i < 100; i++) {
    let state = VillageState.random();
    steps1 += countSteps(state, robot1, memory1);
    steps2 += countSteps(state, robot2, memory2);
  }
  console.log(`Robot 1 uses ${steps1 / 100} steps.`);
  console.log(`Robot 2 uses ${steps2 / 100} steps.`);
}
```
