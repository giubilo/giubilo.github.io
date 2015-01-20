{
    "title": "cmis dlna connector",
    "description": "library to connect cmis compliant repository to dlna devices.",
    "publishdate": "2014-02-01",
    "categories" : [
    	 "summary"
    ]
}

_this page is not finished, see the [[wiki home page|Home]] to find out why..._ 

multiple ways to get to content so can use the tools familiar with to manipulate content e.g. iPhoto or flickr for photos - content at the edge is always tricky - ingesting / manipulating
protocol-based access so don’t get locked in

service bus
design based on a concise set of simple concepts that all can understand and build upon 
exposes a key interface where people can do content-driven-development

content context is built in - because meta-data is a blob as well then can rebuild from scratch an  understanding of content objects just by parsing the blobs - e.g. db backup corrupt, backup manifest corrupt, changing to a new db goes wrong -  never left with just thousands of cut up file names with no way to put back together
ability to back up in a powerful way is built in - has deduplication, sync and share built-in, can use varied cost backup repositories depending on rules e.g. sentimental photos can be backed up on multiple local, peer and cloud sites, large media files that may not be so important can be on local and peer disks - doesn’t have to be one size / cost fits all - its built-in so no separate tools / consoles to manage and because its mutable storage don’t have to worry about piecing incremental backups together - just like git but for content
specific implementation through Docker containers on NAS type devices.  Cloud storage through something like S3 buckets to Glacier lifecycle.

![oauth-flow](/assets/img/allegria-logical-model.png?raw=true)