[![](https://jitpack.io/v/terrierteam/terrier-ciff.svg)](https://jitpack.io/#terrierteam/terrier-ciff)

# Terrier-CIFF

This allows the [Terrier.org information retrieval platform](http://terrier.org) to ingest files written in the [Common Index File Format](https://github.com/osirrc/ciff/) - see [1]. In doing so, a new Terrier index is written.


## Usage

The Terier-CIFF package provides a tool for ingesting files written in the Common Index File Format. It can be used directly from the Terrier commandline (version 5.3 minimum).

```shell
    cd /path/to/terrier
    bin/terrier  -P com.github.terrierteam:terrier-ciff:0.2 ciff-ingest /path/to/ciff.gz
```

This creates a new index at the default location. The standard `-I` option can be used to change the location of the generated index.

## Additional Weighting Models

We provide variants of BM25 that are aligned with those in the Anserini platform. These are as follows:
 - `BM25_log10` - This follows Terrier's standard implementation, but uses log base 10 instead of log base 2.
 - `BM25_log10_nonum` - This removes the unnecessary (k+1) from the BM25 numerator. It alsos uses log base 10.

 For more discussion, see [1] and [2].

## Implementation Notes

 - collection statistics (number of tokens/average document length) are calculated using the document lengths file; we do not consider the collection statistics in the header.
 - we use a shaded version of protobuf 3, as Terrier depends on Hadoop, which includes protobuf 2.5

## Demonstration

We have a notebook demonstrating using terrier-ciff for ingesting a CIFF index into Terrier. It also creates a CIFF file from a Terrier index. This is a [PyTerrier] notebook. It can be run directly using Colab:

 - `trindex_to_ciff.ipynb` : [[Github](https://github.com/terrierteam/terrier-ciff/blob/master/trindex_to_ciff.ipynb)] [[Colab](https://colab.research.google.com/github/terrierteam/terrier-ciff/blob/master/trindex_to_ciff.ipynb)]

## Credits

Craig Macdonald, University of Glasgow

## References

[1] Jimmy Lin, Joel Mackenzie, Chris Kamphuis, Craig Macdonald, Antonio Mallia, Michał Siedlaczek, Andrew Trotman, Arjen de Vries. Supporting Interoperability Between Open-Source Search Engines with the Common Index File Format. In Proceedings of SIGIR 2020. [arXiv:2003.08276](https://arxiv.org/abs/2003.08276).

[2] Which BM25 Do You Mean? A Large-Scale Reproducibility Study of Scoring Variants. Chris Kamphuis, Arjen de Vries, Leonid Boytsov and Jimmy Lin. In Proceedings of ECIR 2020.
