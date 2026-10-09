```
int counter = 0;

int handler( int mid ) {
	int ack, incr, src;

	/* Increment Counter */
	pvm_upkint( &incr, 1, 1 );
	counter += incr;
	printf( "counter = %d\n", counter );

	/* Acknowledge Counter Task */
	pvm_bufinfo( mid, (int *) NULL, (int *) NULL, &src );
	pvm_initsend( PvmDataDefault );
	ack = ( counter > 1000 ) ? -1 : 1;
	pvm_pkint( &ack, 1, 1 );
	pvm_send( src, CNTR_MSGTAG, ctX );
	return( 0 );
}

int main( int argc, char **argv )
{
	int ck, cc, ctx, bufid, incr=1, iter=1, max, numt, old, value=1, src;
	char *args[2];

	/* If I am a Manager Task */
	if ( (cc = pvm_parent()) == PvmNoParent || cc == PvmParentNotSet ) {

		/* Generate New Message Context for Counter Task messages */
		ctx = pvm_newcontext();

		/* Register Message Handler Function for Independent Counter */
		pvm_addmh( -1, CNTR_MSGTAG, ctx, handler );

		/* Spawn 1 Counter Task */
		args[0] = "counter";  args[1] = (char *) NULL;
		old = pvm_setcontext( ctx );  /* Set Message Context for Task */
		if ( pvm_spawn( "example3", args, PvmTaskDefault,
		(char *) NULL, 1, (int *) NULL ) != 1 )
		{
			counter = 1001;  /* Counter Failed to Spawn, Trigger Exit */
			pvm_setcontext( old );  /* Reset to Base Message Context */

			/* Spawn NWORK Worker Tasks */
```
```