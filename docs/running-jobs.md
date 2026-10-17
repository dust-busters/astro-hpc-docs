# Running jobs

!!! tip "Quick reference"
    Check what's running: `top`

    Start a job: `nice -n <NICENESS> program_name <program_arguments>`

There is no scheduler on the astro nodes; everyone shares them by convention. Before launching:

1. **Know your needs.** Estimate memory and CPU, then pick the node group that fits (see [Overview](overview.md)).
2. **Check the load.** SSH into each candidate node and look at `top`.
3. **Launch with `nice`.** It runs your program at a lowered priority.

```bash
nice program_name <program_arguments>          # niceness 10 (default)
nice -n 19 program_name <program_arguments>    # nicest: long, heavy runs
```

Niceness runs from −20 to 19; lower values get priority. Be nicer (higher numbers) for long, CPU-heavy jobs that occupy a node for a long time. Short computations can use a lower niceness.

!!! warning "Always use `nice`"
    The shared setup only works if everyone runs their jobs through `nice`.
