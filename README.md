# Student

Nico Kong (I debugged this alone)

# Shadertoy Link

https://www.shadertoy.com/view/wfsfWf

# Debugging Process

1 - Compiler help me identify that the code wrote
[line 97] vec uv2 instead of vec2 uv2;

2 - starting by looking at the main function, I noticed that uv2 isn't used anywhere, and that is it supposed to be the input for raycast (instead of uv)
[line 100] using uv instead of uv2 as an input;

3 - I noticed that the scene seems stretched. at this point, i decided to start reading the individual subfunctions in order, and noticed that the computation of H seems redundant and was probably a mistake.
[line 11] changed dividing by resolutionY to dividing by resolutionX;

4 - Comparing to the result pic, i noticed the ground isn't rendered as far as it should. with only using 64 steps for the marching, it's not enough for it to reach the full scene. so i changed 
[line 18] to do 256 iterations instead of only 64.

5 - Reflection
i changed it such that when the reflection is not hitting an object, we get a white/black color; and noticed that only a small part of the geometry is changing - this suggests that the reflection rays are hitting something.
I'm now assuming that the reflection is hitting the object itself - since the color is assigned to some material that it hit, but the object still has its own color.
up on further inspection, [line 75] dir = reflect(eye, nor); doesn't make sense.
we're trying to reflect the ray direction and not the eye vector - so I fixed the problem by changing it to
[line 75] dir = reflect(dir, nor);

# lab02-debugging

# Setup 

Create a [Shadertoy account](https://www.shadertoy.com/). Either fork this shadertoy, or create a new shadertoy and copy the code from the [Debugging Puzzle](https://www.shadertoy.com/view/flGfRc).

Let's practice debugging! We have a broken shader. It should produce output that looks like this:
[Unbelievably beautiful shader](https://user-images.githubusercontent.com/1758825/200729570-8e10a37a-345d-4aff-8eff-6baf54a32a40.webm)

It don't do that. Correct THREE of the FIVE bugs that are messing up the output. You are STRONGLY ENCOURAGED to work with a partner and pair program to force you to talk about your debugging thought process out loud.

Extra credit if you can find all FIVE bugs.

# Submission
- Create a pull request to this repository
- In the README, include the names of both your team members
- In the README, create a link to your shader toy solution with the bugs corrected
- In the README, describe each bug you found and include a sentence about HOW you found it.
- Make sure all three of your shadertoys are set to UNLISTED or PUBLIC (so we can see them!)
