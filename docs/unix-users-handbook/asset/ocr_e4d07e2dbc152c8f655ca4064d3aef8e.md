```
break;

default:
	statement;
	statement;
	...
	break;
}
```

The expression enclosed within parentheses is compared against *value_1*, *value_2*, through *value_n*, which must be constants or constant expressions. If a value is found to match the value of the expression, the statements associated with it are executed. If no matches are found, control flows to *default* and its statements are executed.

If I am willing to pay for a car based upon the year it was made, the following switch statement can be used:

```
switch ( car_year )
{
	case 1999:
		printf("I'll offer you $8,000 for the car.\n");
		break;
	case 1998:
		printf("I'll offer you $6,000 for the car.\n");
		break;
	case 1997:
		printf("I'll offer you $3,500 for the car.\n");
		break;
	case 1996:
		printf("I'll offer you $2,100 for the car.\n");
		break;
	case 1995:
		printf("I'll offer you $1,000 for the car.\n");
		break;
	case 1994:
		printf("I'll offer you $800 for the car.\n");
		break;
	case 1993:
		printf("I'll offer you $400 for the car.\n");
		break;
	default:
		printf("No thank you, the car is too old.\n");
		break;
}
```