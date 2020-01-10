# Usage
Rcirc is an user-friendly R package.

## Prediction

## Identify coding ability

## Analysis and Visuallization

### Analysis the type distribution
The circRNA can be devide into seven types based on the different back-splice site. Rcirc can help to

### View the meta-feature
Rcirc can help to veiw the meta-feature of mount of circRNA by the function **showOverview()**, include their distribution, length and so on. In this function, you need to input two parameter: *circbed* and *gff*.  

```
# load the data
circbed = 
gff = 
# analysis 
showOverview(circbed=circbed,gff=gff)
```

### Analysis the reads mapping on sequences


### View the mapping result of single circRNA
Rcirc can also help to view the mapping situation on sequences like IGV by the function **showMapping()**,
