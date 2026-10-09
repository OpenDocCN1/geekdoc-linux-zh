```
//* If I am a Load Monitor Task */
else if ( cc > 0 ) {
   /* Time Simple Computation */
   gettimeofday( &start, (struct timezone *) NULL );
   for ( i=0, value=1.0 ; i < 1000000 ; i++)
      value *= 1.2345678;

   gettimeofday( &end, (struct timezone *) NULL );
   elapsed = (end.tv_usec - start.tv_usec)
         + 1000000 * (end.tv_sec - start.tv_sec);

   /* Dump Into Next Available Message Mbox */
   pvm_initsnd( PvmDataDefault );
   pvm_pkint( &elapsed, 1, 1 );
   index = pvm_putinfo( MSGBOX, pvm_getsbuf(),
            PvmBoxDefault | PvmBoxPersistent
            | PvmBoxMultiInstance | PvmBoxOverWritable );

   /* Free Next Mbox Index for Next Instance (Only Save 10) */
   pvm_delinfo( MSGBOX, (index + 1) % 11, PvmBoxDefault );
}

   pvm_exit();

return( 0 );
}
```