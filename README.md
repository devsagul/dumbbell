# dumbbell

Training log processor

# Training logs

I am using old school pen and paper method to log my workouts, so I have to use some kind of format, that
allow me to transfer my notes without causing too much troubles. Examples of my these notes can be found 
in the `examples` directory.

There are several things I have to accomodate to:

- There are different variations of the same excercise (e.g. different handles on a pulldown machine, weighted/bodyweight excercises, etc.)
- There can be supersets and dropsets
- For the most part though there are plain regular sets with weights
- Cardio excercises are measured by distance or duration
- Cardio excercises have difficulty levels
- Some machines use levels instead of weights
- Some machines have blocks on them, so weights can be halved or quartered

I want to stick to raw data with as much detail as possible without overcomplicating the log structure (so it would be easy to fill in). On the other hand, these logs have to be structured not to overcomplicate processing logic.

## Data format

- A double-dash (`--`) is used to mark any rest points. For the most part any set will be marked with a double dash on two sides, but this allows to write down dropsets as two or more different records with different weights without a dash between them. 
Hypothetically, it can be used to log supersets, although it whould be really hard to analyze, so I use a single dash to mark
short pause (like the one I need to change the machines) without full rest.
- By default weight excercise is assumed, any cardio excercises are marked by [C] in the begginning of the record.
- Then I add the name of the excercise in the free form.
- Then I mark the end of the name by semicolon (`;`) and add additional info.
- To mark the reps I use `reps:X` or `r:X` where `X` is the number of reps.
- To mark the weights I use `w:X:<scale>[:qualifier][:e]` or `weight:X:<scale>[:qualifier]`, scale can be in `kg`, `lbs` or `lvl`, 
but I try to avoid using `lvl` if possible, `qualifier` is optional and can be either `h` for halved weights or `q` for 
quartered weights. There is also a special mark `:e` to mark that the weights are applied to each limb in the excercies
where it's applicable. By default the total weight is assumed, although it can make little sense for alternating excercises,
I think it's easier to just add `:e` for clarity.
- For barbell excercies the barbell is included in the weights.
- For smith machine the barbell is not included in the weights, because it's easier to track progress with added weights on these excercies.
- To mark duration I use `d:<duration>`.
- The name of the excercise can be ommited by using `~` to refer to the previous excercise. Same with any additional qualifiers, although they have to be listed (e.g. `w:~`).
- If log entry is absolutely the same as the last one, `~~` can be used to mark that. Alternatively, `~` can be used at the and of the current log entry, for each `~` used one more entry should be added with a `--` pause assumed.
- For cardio excercises level assumes speed in kmh if applicable (or difficulty level) and is marked by `l:X`, target BPM is 
marked by `bpm:X`, and elevation is marked in `e:X`.
- Any other marking can be added e.g. `grip:narrow` to account for excercise variants.
