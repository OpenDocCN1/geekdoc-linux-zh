
```c
165: pts.c_cflag |= HUPCL;
166: pts.c_cc[VMIN] = 1;
167: pts.c_cc[VTIME] = 0;
168:
169:   * 标准 CR/LF 处理：这是一个哑终端。
170:   * 不进行翻译：
171:     * 输出时不不将 NL 映射为 CR/NL，
172:     * 输入时不不将 CR 映射为 NL。
173:   */
174: pts.c_oflag &= ~ONLCR;
175: pts.c_iflag &= ~ICRNL;
176:
177:   * 现在处理本地终端侧 */
178: tcgetattr(STDIN_FILENO, &sts);
179:   s = sts;
180:   * 再次，一些任意操作 */
181: sts.c_iflag &= ~BRKINT;
182: sts.c_iflag |= IGNBRK;
183: sts.c_iflag &= ~ISIG;
184: pts.c_cc[VMIN] = 1;
185: pts.c_cc[VTIME] = 0;
186: sts.c_iflag &= ~ICANON;
187:   * 无本地回显：允许另一端进行回显 */
188: sts.c_iflag &= ~(ECHO | ECHOL);
189:
190: optCon = poptopt("robin", argc, argv, optionsTable, 0);
191:
192:   * 选项处理现在将修改 pts 和 sts */
193:   while ((c = poptNextOpt(optCon)) >= 0) {
194:     switch (c) {
195:       case 'H':
196:         usage(0, NULL, NULL);
197:         break;
198:       case 'c':
199:         /* / 随 NL发送 CR */
200:         pts.c_oflag |= ONLCR;
201:         break;
202:       case 'h':
203:         /* / 硬件流控 */
204:         pts.c_cflag |= CRTSCTS;
205:         pts.c_iflag &= ~(IXON | IOFF | IXANY);
206:         break;
207:     case 's':
208:       /* 软件流控 */
209:       pts.c_cflag &= ~CRTSCTS;
210:       pts.c_iflag |= IXON | IXOFF | IXANY;
211:       break;
212:     case 'n':
213:       /* 无流控 */
214:       pts.c_cflag &= ~CRTSCTS;
215:       pts.c_iflag &= ~(IXON | IOOFF | IXANY);
216:         break;
217:     }
218:   }
219: 
220:   if (c < -1) {
221:     /* 选项处理期间发生错误 */
222:     fprintf(stderr, "%s\n",
223:       popoptBadoption(opt, POPT_BADOPTION_NOALIAS),
224:       strerror(c));
225:     return 1;
226:   }
227: 
228:   /* 除非指定了 -b，否则速率不会修改 */
229:   if (speed) {
230:     tcfsetispeed(&pts, symbolic_speed(speed));
231:     tcfsetispeed(&pts, symbolic_speed(speed));
232:   }
233: 
234:   /* 设置信号处理器以恢复旧的
235:    * termios 处理器 */
236:   sact.sa_handler = cleanup_termios;
237:   sigaction(SIGHUP, &sact, NULL);
238:   sigaction(SIGINT, &sact, NULL);
239:   sigaction(SIGPIPE, &sact, NULL);
240:   sigaction(SIGTERM, &sact, NULL);
241: 
242:   /* 现在设置修改后的 termios 设置 */
243:   tcsetattr(pf, TCSANOW, &pts);
244:   tcsetattr(STDIN_FILENO, TCSANOW, &sts);
245: 
246:   do (
247:     FD_ZERO(&ready);
248:     FD_SET(STDIN_FILENO, &ready);
249:     FD_SET(pf, &ready);
250:     select(pf+1, &ready, NULL, NULL, NULL);
251:     if (FD_ISSET(pf, &ready)) {
252:       /* pf 有字符供我们使用 */
253:       i = read(pf, buf, BUFSIZE);
254:       if (i >= 1) {
...
```
