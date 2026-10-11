```
Listing 10.5: continued
217:     return -1;
218:
219:     rpn_pop(&opr1);
220:     rpn_pop(&opr2);
221:
222:     if ( mpz_size_t(*opr2) > 1 )
223:         /* Too many limbs in size */
224:         return -1;
225:
226:     reps = mpz_get_si(*opr2);
227:     if ( reps < 1L || reps > 32768L )
228:         /* Too large for opr2 */
229:         return -1;
230:
231:     z = mpz_probab_prime_p(*opr1,reps);
232:     mpz_set_si(*opr1,(long)z);
233:     rpn_free(&opr2);
234:
235:     return rpn_push(opr1);
236: }
237:
238: /*
239:  * Operation "genprime":
240:  *
241:  * Generate a random prime number.
242:  *
243:  * OPERANDS:
244:  *   1. The modulo value to apply
245:  *      to the randomizing value
246:  *      (see "random").
247:  *   2. The number of primality
248:  *      tests to perform (typically
249:  *      this value is 25).
250:  * RESULTS:
251:  *   1. The randomly generated high
252:  *      number (actually, only a high
253:  *      probability of being prime).
254:  */
255: static int
256: rpn_genprime(void) {
257:     mpz_t *opr1;
258:     mpz_t *opr2;
259:     mpz_t *res;
260:
261:     if ( sp < 2 )
262:         return -1;
```