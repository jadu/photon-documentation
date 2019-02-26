# Troubleshooting

**The site is complaining that the theme doesn't exist**

This is commonly down to either the theme service not being defined within the theme bundle `services.yml`, or the DependencyInjection folder and it's related files being missing from the theme bundle.

**My template file isn't overriding the original template file**

Generally this is down to differences in the path to the file. Double check that the files names match exactly, as this is case sensitive. Check that the directory path to the two templates is an exact match.