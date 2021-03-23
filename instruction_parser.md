## Outline for Parsing and Executing Instructions for Exterior Control of Drone Performance
##### Building out this feature to provide flexibility for us to house exterior logic to decide how the drone should operate and execute the instructions on PX4.
### Component Overview
  1. Choose an Adequate data interchange format to succinctly express the desired behavior in a replicatable manner.
      - JSON will be used to store the command sequence that should be executed
      - Verbage to match operations to commands must be hashed out and any specifics such as location must also be defined
        - Example Format:
                        {"command": Takeoff},{"command": Deliver, "location": "95.6,123.4"}
  2. Write Format Parsing code to read in inputs and translate to decisions by commander
  3. Identify location in execution flow to house logic
      - Edit Custom Command Method in Commander to add logic for other requisite commands such as Deliver
      - Trigger Custom Command method from run method of commander
      - Publish uOrb status 'exterior_commands' and subscribe to this topic from commander. Read the values that are published and trigger the custom command
        - Have setup script launch JSON parsing code and publish to uORB under the exterior_commands topic, which will then be picked up by commander and executed in the rest of the flow. From here on out we can then build more commands to be executed.

**This is a rough proposal for the implementation of performance using exterior commands and will continue to be iterated upon and updated as the implementation gets further. Initial pseudocode for this proposal has been written and will be added in future PRs.**
