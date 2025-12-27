## ExpNo:10 Implementation of Classical Planning Algorithm 

## NAME: PREM PRASANTH J
## REG NO: 2305001028
## Algorithm or Steps Involved:
Define the initial state
Define the goal state
Define the actions
Find a plan to reach the goal state
Print the plan

### Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
Output:
['move_A_to_B']
```

### Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
Output:
['move_A_to_B', 'move_B_to_C']
```

### PROGRAM
```
    def is_goal_state(current_state, goal_state):
    return current_state == goal_state


def apply_action(current_state, action_effect):
    new_state = current_state.copy()
    new_state.update(action_effect)
    return new_state


def is_applicable(current_state, precondition):
    return all(current_state.get(key) == value for key, value in precondition.items())


def find_plan(initial_state, goal_state, actions):
    queue = [(initial_state, [])]
    visited_states = set()

    while queue:
        current_state, partial_plan = queue.pop(0)

        # Goal test
        if is_goal_state(current_state, goal_state):
            return partial_plan

        state_tuple = tuple(sorted(current_state.items()))
        if state_tuple in visited_states:
            continue

        visited_states.add(state_tuple)

        for action in actions:
            if is_applicable(current_state, actions[action]['precondition']):
                next_state = apply_action(current_state, actions[action]['effect'])
                queue.append((next_state, partial_plan + [action]))

    print("No plan exists.")
    return None


# ----------------------------------------------------------
# TEST 1
# ----------------------------------------------------------
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}
actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)      # EXPECTED: ['move_A_to_B']


# ----------------------------------------------------------
# TEST 2
# ----------------------------------------------------------
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}
actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)      # EXPECTED: ['move_A_to_B', 'move_B_to_C', 'move_C_to_Table']


# ----------------------------------------------------------
# TEST 3
# ----------------------------------------------------------
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'Table', 'B': 'Table'}
actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)      # EXPECTED: []

```

### OUTPUT
<img width="381" height="175" alt="image" src="https://github.com/user-attachments/assets/382cd5b3-0654-4151-84c5-b88c30c15b84" />

## RESULT
Thus the program to implement Classical Planning Algorithm has been executed successfully.
