# TreeBot framework for deno/node


## Example:
```typescript
import { TreeBot, TreeTask, BranchTask, LeafTask } from './mod.ts'

class IsSunday extends BranchTask {
  validate() {
    return (new Date().getDay()) === 0
  }

  successTask() {
    return new LogSunday();
  }

  failureTask() {
    return new LogNotSunday();
  }
}

class LogSunday extends LeafTask {
  execute() {
    console.log('Its sunday today!')
  }
}

class LogNotSunday extends LeafTask {
  execute() {
    console.log('Its not sunday today!')
  }
}

class ExampleBot extends TreeBot {
  createRootTask(): TreeTask {
    return new IsSunday();
  }

  onLoop() {
    console.log("Loop!!");
  }

  onStart() {
    console.log("Started");
  }
}

const bot = new ExampleBot();
bot.run();
```
