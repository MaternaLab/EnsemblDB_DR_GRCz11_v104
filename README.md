# EnsemblDB Danio rerio GRCz11 v104

R package for an Ensembl database for Danio rerio GRCz11 v104

This package was used for the snATAC-seq study: XXXX


## Generate the package from scratch
Here is the code used to generate the database package

    ## load the packages
    library(AnnotationHub)
    library(ensembldb)
    
    ## Load the annotation resource.
    ah <- AnnotationHub()

    ## Query for all available EnsDb databases
    query(ah, "EnsDb")

    ahDb <- query(ah, pattern = c("Danio rerio", "GRCz11", 104))
    
    ## Quick check
    ahDb

    ## Get the resource for the gtf file with the gene/transcript definitions.
    Gtf <- ahDb["AH92019"]
    
    ## Create a EnsDb database file from this.
    DbFile <- ensDbFromAH(Gtf)
    
    ## We can either generate a database package, or directly load the data
    edb <- EnsDb(DbFile)

    makeEnsembldbPackage(ensdb = DbFile, version = "0.0.1",
                         maintainer = "Oscar Davalos <myemail@email>",
                         author = "O Davalos")
