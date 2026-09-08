## Assignment 1: Chromosome Structures
Assignment Date: Wednesday, September 9, 2026 <br>
Due Date: Wednesday, Sept. 16, 2026 @ 11:59pm <br>

### Assignment Overview

In this assignment you will profile the overall structure of the genomes of several important species and then study human chromosome 22 in more detail.
As a reminder, any questions about the assignment should be posted to [Piazza](https://piazza.com/jhu/fall2026/600449600649).

### Question 1: Why Genomics? [5 pts]

- Question 1.1. Use ChatGPT (or your favorite LLM) to write an essay on why you are interested in genomics. Include specific details from your own interests. Make sure to ask for references. Make sure to include both your prompt(s) and the output from the LLM

- Question 1.2. Comment on the output from the LLM - does it make logical sense, does it include any phrases you would not have written, do the cited papers exist and support the claims from the LLM?

- Question 1.3 Post your final prompt, the LLM's response, and which LLM you used to piazza. Include the link to the post in your submission


### Question 2: Chromosome structures [10 pts]

Download the chromosome size files for the following genomes (Note these have been preprocessed to only include main chromosomes):

1. [E. coli (Escherichia coli K12)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/ecoli.chrom.sizes) - One of the most commonly studied bacteria [[info]](https://en.wikipedia.org/wiki/Escherichia_coli)
2. [Yeast (Saccharomyces cerevisiae, sacCer3)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/yeast.chrom.sizes) - an important eukaryotic model species, also good for bread and beer [[info]](https://en.wikipedia.org/wiki/Saccharomyces_cerevisiae)
3. [Worm (Caenorhabditis elegans, ce10)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/ce10.chrom.sizes) - One of the most important animal model species [[info]](https://en.wikipedia.org/wiki/Caenorhabditis_elegans)
4. [Fruit Fly (Drosophila melanogaster, dm6)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/dm6.chrom.sizes) - One of the most important model species for genetics [[info]](https://en.wikipedia.org/wiki/Drosophila_melanogaster)
5. [Arabidopsis thaliana (TAIR10)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/TAIR10.chrom.sizes) - An important plant model species [[info]](https://en.wikipedia.org/wiki/Arabidopsis_thaliana)
6. [Tomato (Solanum lycopersicum v4.00)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/tomato.chrom.sizes) - One of the most important food crops [[info]](https://en.wikipedia.org/wiki/Tomato)
7. [Human (hg38)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/hg38.chrom.sizes) - us :) [[info]](https://en.wikipedia.org/wiki/Homo_sapiens)
8. [Wheat (Triticum aestivum, IWGSC)](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/wheat.chrom.sizes) - The food crop which takes up the largest land area [[info]](https://en.wikipedia.org/wiki/Wheat)

Using these files, make a table with the following information per species (Recall the N50 length is the length such that 50% of the genome is in chromosomes of this size or larger):

- Question 2.1. Total genome size

- Question 2.2. Number of chromosomes

- Question 2.3. Largest chromosome size and name

- Question 2.4. Smallest chromosome size and name

- Question 2.5. Mean chromosome length

- Question 2.6. N50 chromosome length


### Question 3. Random DNA shearing and fragment lengths [20 pts]

Before sequencing, DNA is often broken into smaller fragments. In this question, you will simulate randomly cutting a 1Mbp genome and examine the lengths of the fragments that remain. You do not need to simulate the DNA sequence itself.

- Question 3.1. In the language of your choice, simulate cutting a linear 1Mbp genome into 10,000 segments by picking 9,999 distinct cut points uniformly at random from positions 1 through 999,999. A cut at position x is between bases x and x+1. Sort the cut points, include the two ends of the genome, and compute the length of each remaining fragment. Report the mean fragment length. Plot a histogram of the fragment lengths and overlay an exponential distribution using the mean you just computed (lambda = 1/mean). How well does the exponential distribution fit the data (just a visual comparison is enough)? Here is pseudocode for the simulator:

```
genomesize = 1000000
num_segments = 10000

## sample distinct cut positions without replacement
cut_points = random_sample_without_replacement(1, genomesize-1, num_segments-1)
boundaries = concatenate([0], sort(cut_points), [genomesize])
fragment_lengths = initialize_empty_list()

for (i = 0; i < num_segments; i++)
{
  length = boundaries[i+1] - boundaries[i]
  append(fragment_lengths, length)
}

mean_length = mean(fragment_lengths)

## now plot the histogram and overlay the exponential distribution
...
```

  - Note: Normalize your histograms as probability densities (total area = 1) so that you can compare them with the fitted distributions. Label the x-axis with length in bp and the y-axis with probability density.

- Question 3.2. Keep the fragments in their original order along the genome and divide them into non-overlapping groups of 10: fragments 1-10, 11-20, 21-30, etc. Compute the total length of each group, giving 1,000 observations. Plot a histogram of these total lengths and fit a negative binomial distribution using r = 10 and p = 10 divided by the observed mean group length. Overlay the fitted distribution. How well does it fit (just a visual comparison is enough)? How does the shape of this histogram compare with the histogram of individual fragment lengths?

  - Hint: To plot the fitted probability for a total length s, use `scipy.stats.nbinom.pmf(s - 10, n=10, p=p)` in Python or `dnbinom(s - 10, size=10, prob=p)` in R. The subtraction of 10 converts the total length to the number of uncut positions before 10 cuts. For a binned histogram, sum the predicted probabilities over the integer lengths in each bin and divide by the bin width to match the histogram's density scale. Because we fix the number of cuts in a finite genome, the exponential and negative binomial curves are approximations.

- Question 3.3. Repeat Questions 3.1 and 3.2, this time cutting the same 1Mbp genome into 100,000 segments. Report the mean fragment length and the mean total length of a group of 10. Show both histograms with their fitted distributions, using the new means to set the parameters. How do the lengths and the quality of the fits compare with your results for 10,000 segments?

- Question 3.4. How many cuts should you make in a linear 1Mbp genome so that the mean fragment length is as close as possible to 42bp? Remember that the number of fragments is one more than the number of cuts. Report the integer number of cuts and the resulting mean fragment length.

- Question 3.5. Run the simulator from Question 3.1 using the number of cuts you calculated in Question 3.4. Report the mean fragment length and show both histograms: individual fragment lengths with a fitted exponential distribution, and total lengths of non-overlapping groups of 10 with a fitted negative binomial distribution. If fewer than 10 fragments remain at the end, omit those fragments from the grouped histogram only. How well do the fitted distributions describe your results?


### Question 4. Coverage simulator [20 pts]

- Question 4.1. How many 100bp reads are needed to sequence a 1Mbp genome to 3x coverage?

- Question 4.2. In the language of your choice, simulate sequencing 3x coverage of a 1Mbp genome with 100bp reads and plot the histogram of coverage. Note you do not need to actually output the sequences of the reads, you can just uniform randomly sample positions in the genome and record the coverage. You do not need to consider the strand of each read. The start position of each read should have a uniform random probability at each possible starting position (1 through 999,901). You can record the coverage in an array of 1M positions. Overlay the histogram with a Poisson distribution with lambda=3. Also overlay the distribution with a Normal distribution with a mean of 3 and a standard deviation of 1.73 (which is the square root of 3). Here is the pseudocode for the simulator:

```
num_reads = calculate_number_of_reads(genomesize, readlength, coverage)

## use an array to keep track of the coverage at each position in the genome
genome_coverage = initialize_array_with_zero(genomesize)

for (i = 0; i < num_reads; i++)
{
  startpos = uniform_random(1,genomesize-readlength)
  endpos = startpos + readlength - 1
  for (x = startpos; x <= endpos; x++)
  {
    genomecoverage[x] = genomecoverage[x] + 1
  }
}

maxcoverage = max(genomecoverage)

## use an array count how many positions have 0x coverage, have 1x coverage, have 2x coverage, ...
histogram = initialize_array_with_zero(maxcoverage)

for (x = 0; x < genomesize; x++)
{
  cov = genomecoverage[x]
  histogram[cov] = histogram[cov] + 1
}

## now plot the histogram
...

```

- Question 4.3. Using the histogram from Q4.2, how much of the genome has not been sequenced (has 0x coverage)? How well does this match Poisson expectations? How well does the normal distribution fit the data?

- Question 4.4. Now repeat the analysis with 10x coverage: 1. simulate the appropriate number of reads, 2. make a histogram, 3. overlay a Poisson distribution with lambda=10, 4. overlay with a Normal distribution with mean=10, standard deviation=3.16 (sqrt(10)). 5. compute the number of bases with 0x coverage, and 6. evaluate how well it matches the Poisson expectation and Normal expectations.

- Question 4.5. Now repeat the analysis with 30x coverage: 1. simulate the appropriate number of reads, 2. make a histogram, 3. overlay a Poisson distribution with lambda=30, 4. overlay with a Normal distribution with mean=30, standard deviation=5.47 (sqrt(30)). 5. compute the number of bases with 0x coverage, and 6. evaluate how well it matches the Poisson expectation and Normal expectations.




### Question 5: Kmer Uniqueness [20 pts]

Download the human chromosome 22 from here: [https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/chr22.fa.gz](https://schatz-lab.org/appliedgenomics2026/assignments/assignment1/chr22.fa.gz)

#### Notes:

- A kmer is a substring of length k. For example, the string GATTACA, has these 3-mers: GAT, ATT, TTA, TAC, ACA

- A string of length G has G - k + 1 kmers. For long strings, G - k + 1 is nearly the same as G e.g. for human using 19mers, 3,000,000,000 vs 2,999,999,986

- While a string of length G has G-k+1 kmers, there may be many fewer *distinct* kmers. For example, in the string "GCATCATCATCATCATCATCAT..." the kmers are: GCA, CAT, ATC, TCA, CAT, ATC, TCA, CAT, ATC, TCA, CAT, ... As such there are only 4 distinct kmers (GCA, CAT, ATC, TCA). Of these GCA occurs once and the others occur many times.

- If your computer runs out of RAM, you can use a portion of chromosome22 (e.g the first 20Mbp or smaller region). Just make to to mark which portion of the chromosome you are using. Also make sure that this region is not just N characters.

#### Questions:

- Question 5.1. How many As, Cs, Gs, Ts are found in the entire chromosome? What other characters are found and how often are they found?

- Question 5.2  Write a script to clean a fasta file by ensuring all characters are in uppercase ("a" becomes "A") and replacing any non-ACGT characters with "A" (especially N characters). Run this script on chr22 and report how many As, Cs, Gs, and Ts are now found

- Question 5.3. In the language of your choice, tally the frequency of 19-mers in the cleaned chromosome file, and output the kmer frequency spectrum to a file e.g. how many kmers occur 1 time, how many occur 2 times, how many occur 3 times, etc. We recommend you use a dictionary (or hash table) to tally the frequencies using this pseudocode. In your writeup, show the kmer frequency spectrum for 1 to 20, e.g. how many kmers occur 1 time, how many occur 2, ..., how many occur 20 times. Note you should record all values in the file (up to max_frequency), but in your write up only display the first 20 (e.g. with the unix `head` command)

```
## initialize kmer length
k=19

## read genome, convert to upper canse and convert non-DNA to 'A'
genome_string = read_from_file("chr22.fa")

## dictionary that maps a kmer (like GAT) to a frequency (like 3)
kmer_frequency = initialize_dictionary()

## now scan the genome, extract kmers, and tally up their frequencies
for(i = 0; i < length(genome_string) - k + 1; i++)
{
  kmer = substring(genome_string, i, k)
  kmer_frequency[kmer] = kmer_frequency[kmer] + 1
}

## now tally the frequencies in a dictionary that maps kmer frequency to count
## also determine the maximum kmer frequency

tally = initialize_dictionary()
all_kmers = kmer_frequency.keys()
max_frequency = 0

for (i = 0; i < length(all_kmers); i++)
{
  kmer = all_kmers[i]
  freq = kmer_frequency[kmer]
  tally[freq] = tally[freq] + 1

  if (freq > max_frequency)
  {
    max_frequency = freq
  }
}

## now print in sorted order
for (i = 1; i <= max_frequency; i++)
{
  if (tally.has_key(i))
  {
    freq = tally[i]
    print_to_file(i, freq)
  }
}
```

- Question 5.4. Using the output from 5.3, plot the kmer frequency spectrum: x-axis is the kmer frequency, and the y-axis is the number of kmers that occur x times. Make sure to plot both the x and y-axis in log space. This should include all kmers (up to max_frequency)

- Question 5.5. a) What percent of the genome is unique, e.g. what percent of the kmers occur 1 time. b) What percent of the genome is repetitive (occurs more than 1 time). c) What percent occurs 1000 or more times?

  - Note: For this analysis, you should separately consider all of the kmers in the genome, e.g. the denominator will be G-k+1. When computing the unique percentage, use the number of unique kmers as the numerator. When computing repetitive percentages, make sure to separately count each instance of a repetitive kmer. For example the string "GCATCATCAT" has kmers: GCA, CAT, ATC, TCA, CAT, ATC, TCA, CAT. Of these 1/8 (12.5%) are unique and 7/8 (87.5%) are repetitive



### Hints

- We highly recommend you use [Jupyter notebooks](https://jupyter.org/) that you can then "print" to a PDF. If you have issues printing to PDF, export to HTML, and then print to PDF.
- Many of the questions can be addressed with standard command line [tools](http://lh3lh3.users.sourceforge.net/biounix.shtml) such as `grep`, `wc`, `awk`, `sort`, `fold`, etc
- You may wish to try out [`datamash`](https://www.gnu.org/software/datamash/)
- You may find [`samtools`](http://www.htslib.org/) and especially `samtools faidx` helpful for indexing the fasta files
- Plotting can be done in any language; R or Python are recommended; Excel is okay but ugly :-P
- Be sure to clearly mark each question and subquestion in the PDF and then highlight each question in GradeScope
- If your laptop runs out of RAM for question 5, you can consider the first 1Mbp or 10Mbp of the genome. Just be sure to mark what part of the genome you considered




### Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and 
all relevant figures (as needed). Make sure to clearly label each of the subproblems and give the exact commands and/or code snippets you used for solving the question. Submit your solutions by uploading the PDF to [GradeScope](https://www.gradescope.com/courses/1370921) (Entry code: 7B4VJ6), and remember to select where in your submission each question/subquestion is. 

If you submit after this time, you will start to use up your late days. Remember, you are only allowed 96 hours (4 days) for the entire semester!



