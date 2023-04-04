Suggestions to myself to improve the [fragments](https://github.com/saevrenk/fragments.git) code:

1. Add more comments to the code to explain what each part does. 

2. Add error handling to handle situations where the input data is not in the expected format, or where there are errors in the RDKit processing steps. For example, you could add try/except blocks around the RDKit functions to catch any errors that are raised.

3. Refactor the code to make it more modular and reusable. For example, you could define a separate function to read in the input data, another function to extract the fragments from the SMILES, and a third function to plot the most common fragments.

4. Use argparse to handle command-line arguments in a more user-friendly way. This would allow users to specify the input file, output file, number of fragments to display, etc., without having to modify the code.

