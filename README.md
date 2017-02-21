![alt tag](https://raw.githubusercontent.com/AshokHub/BLASTphp/misc/BLASTphp_Logo_500px.png)
    
# [About](https://github.com/AshokHub/BLASTphp/blob/master/README.md)
The [BLASTphp](https://github.com/AshokHub/BLASTphp) is a PHP library for the [NCBI BLAST Common URL API](https://ncbi.github.io/blast-cloud/dev/api.html). It allows you to run [NCBI BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) remotely through RESTful services. BLASTphp requests to NCBI BLAST URI and elicits a response in HTML, Text, XML, XML2, JSON2, or Tabular (text) format. The default response format is HTML.

# [Usage](https://ncbi.github.io/blast-cloud/doc/running-web-blast.html)
Please refer to [NCBI BLAST Cloud Documentation](https://ncbi.github.io/blast-cloud/) for detailed information.

To use BLASTphp, first set the maximum execution time of webserver to request time of execution (RTOE) value of BLAST, because the default maximum execution time (30 seconds) is not enough. For example:

    ini_set('max_execution_time', $RTOE);

In some cases `$RTOE` is not enough to execute the program. If so, you must increase the `$RTOE` to `$RTOE+60`. A `max_execution_time` value of 0 will make the max execution time to unlimited. However, it is not recommended that you do this. In rare cases in which a script has somehow gone into an infinite loop, or is in a deadlock because of file level locking, your server will get overloaded and your memory and CPU usage will go above recommended thresholds.

# [Example](https://github.com/AshokHub/BLASTphp#example)
## [Connecting to NCBI BLAST Server](https://github.com/AshokHub/BLASTphp#connecting-to-ncbi-blast-server)
The following is an example script that can be executed on the command-line. It is contained in the examples directory of this repository and named 'check_job_status.php'.  Typically PHP scripts are not used on the command-line but here we do so for the sake of demonstration.  The following script receives as its first argument the API key of a user on the public BLAST server at https://biogem.org.  It authenticates the user using the API key, queries the remote server to find the list of workflows that the user has created and prints the names of those workflows.

    <?php
    
    // Include the BLASTphp library.
    require_once('../blast.inc');
    
    // The domain name of the host to connect to.
    $hostname  = 'biogem.org';
    // Port 443 is the typical port for HTTPS.
    $port      = '443';
    }

# [Usage Guidelines](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=DeveloperInfo)
Do not overload the NCBI servers. If you are intending to perform more than 20 searches in a session you should comply with the following guidelines:

1. Do not contact the server more often than once every three seconds.
2. Do not poll for any single RID more often than once a minute.
3. Use the URL parameter email, and tool, so that we can track your project and contact you if there is a problem.
4. Run scripts weekends or between 9 pm and 5 am Eastern Time weekday if more than 50 searches will be submitted.

BLAST often runs more efficiently if multiple queries are sent as one search than if each query is sent as an individual search. This is especially true for blastn, megablast, and tblastn. If your queries are short (less than a few hundred bases) we suggest you merge them into one search of up to 10,000 bases.

The NCBI servers are a shared resource and not intended for projects that involve a large number of BLAST searches. Stand-alone BLAST and the RESTful API at a cloud provider are provided for such projects.
	
# [License](https://github.com/AshokHub/BLASTphp/blob/master/LICENSE)
BLASTphp is made available under version 3 of the GNU Lesser General Public License.
