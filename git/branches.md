### Branching
- Multiple `pointer` to single commit
- We can work on specific feature/functionality 
- Can retrieve(cherry-pick/merge) required changes from other branches for testing or enhancing your feature
- Let's have Server `A` and `B`, communicating with each other. If you want changes in `A`, and `A`-`B` communication must be goes on. `A` is well working on it's current version (new changes may affect communication). Should make ```new_working ``` branch for doing new stuff instead of ```stable``` branch. 

### Merge
```git merge``` combine changes with other branch lets say
- ```$ git merge new_work```
- ```merge``` make **one** commit

### Merge conflict
When different changes in both merging branches at same HEAD.
