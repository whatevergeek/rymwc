Creating your first patch - Hello, World!
Let’s start with a simple sine-wave patch with a gain control, to demonstrate how to create a custom processor, connect it up inside a graph, and provide a parameter to control something from the GUI.

Step 1 - Create a New Patch
Start by using the command-line app to create a new, empty patch:

$ cmaj create AnnoyingBeep
This creates a basic patch in a folder called “AnnoyingBeep”. If you have a look inside at the file called AnnoyingBeep.cmajor, it’ll look something like this:

graph AnnoyingBeep  [[main]]
{
    output stream float out;

    node sine = std::oscillators::Sine (float, 440);

    connection sine -> std::levels::ConstantGain (float, 0.15f) -> out;
}
If you start the patch running with:

$ cmaj play AnnoyingBeep/AnnoyingBeep.cmajorpatch

---
https://mudloop.github.io/cmajor-playground/