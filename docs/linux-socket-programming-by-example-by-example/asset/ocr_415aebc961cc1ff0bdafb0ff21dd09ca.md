# Listing 18.2: continued

```
				62:		 */
				63:		#define DTLEN					10
				64:
				65:		 */
				66:		* Time field length:
				67:		 */
				68:		#define TMLEN					7
				69:
				70:		 */
				71:		* Define TRUE & FALSE if not defined:
				72:		 */
				73:		#ifndef TRUE
				74:		#define TRUE				1
				75:		#define FALSE				0
				76:		#endif
				77:
				78:		 */
				79:		* Ticker Request Structure:
				80:		 */
				81:		typedef struct {
				82:			char	ticker[TICKLEN+1];	/* Symbol */
				83:			double	last_trade;			/* Last Price */
				84:			char	*date;			/* Date */
				85:			char	*time;			/* Time of Last Trade */
				86:			double	change;			/* */
				87:			double	open_price;		/* Opening Price */
				88:			double	high;			/* High Price */
				89:			double	low;				/* Low Price */
				90:			double	volume;			/* Volume of Trades */
				91:			int	flags;			/* Server flags */
				92:			time_t	next_samp; /* Time of next evt */
				93:		} TickReq;
				94:
				95:		 */
				96:		* Ticker Flags:
				97:		 */
				98:							/* Ticker unknown */
				99:		#define FLG_UNKNOWWN			1
				100:					/* Data format error */
				101:		#define FLG_ERROR			2
				102:
				103:		 */
				104:		* External Function References:
				105:		 */
				106:	extern int load(
				107:			TickReq *tick,int *pntick,int nmax);
```