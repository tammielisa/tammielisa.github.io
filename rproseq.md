# R: Visualize Amino Acid Frequencies in a Protein

I want to import a pdb file from the Protein Data Bankinto R, display the protein sequence, 
and make a visualization showing the frequencies of each amino acid. I want to use ggplot2 
to do the visualization. The amino acid labels should display as three letter codes instead
of one letter. Instead of the labels appearing as ticks along the x axis, I want them to 
sit on top of the bars in the chart.

Note: ChatGPT gave a function pdb2seq to extract the protein sequence, but it appears to
not exist. Function pdbseq, shown in the code, works. The aa1 = FALSE gives the three letter
codes instead of one letter.

***ChatGPT***
*I can help you with that. To import a PDB file into R, you can use the bio3d package, 
which is a useful tool for working with biological structure data. You can create 
a more customizable and aesthetically pleasing plot using the ggplot2 package. 
Here's an example of how to visualize the amino acid frequencies with ggplot2*

```r
library(bio3d)
library(ggplot2)

pdb <- read.pdb("path/to/your/file.pdb")

print(pdb)

# Get the protein sequence
protein_seq <- pdbseq(pdb, aa1 = FALSE)
print(protein_seq)

# Create a data frame for ggplot
aa_counts <- data.frame(AminoAcid = names(table(protein_seq)), Frequency = as.numeric(table(protein_seq)))

# Create a bar plot with ggplot2
ggplot(aa_counts, aes(x = AminoAcid, y = Frequency, fill = AminoAcid)) +
  geom_bar(stat = "identity") +
  geom_text(aes(label = AminoAcid), position = position_stack(vjust = 1.1), color =          "black", size = 3) + 
  scale_x_discrete(labels = NULL, breaks = NULL) + 
  scale_fill_manual(values = rainbow(20)) +
  labs(title = "Amino Acid Frequencies", x = " ", y = "Frequency") +
  theme_minimal() +
  guides(fill = FALSE) +
  theme(axis.ticks.x = element_blank())  # Hide both x-axis text and ticks

```

Resulting image:

