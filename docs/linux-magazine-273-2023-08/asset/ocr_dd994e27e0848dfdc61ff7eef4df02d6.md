# Listing 1: scoreboard.py (continued)

```
270 def processGameSelect( self, gameID ):
271 cursor = self.db.cursor( pysqlite2.cursors.DictCursor )
272 sql = "SELECT t1.teamName AS t1name, t2.teamName AS
 t2name, games.* FROM games LEFT JOIN teams\ t1
 ON t1.ID=game.team1 LEFT JOIN teams\ t2 ON t2.
 ID=game.team2 WHERE games.ID = " + str( gameID )
273 cursor.execute( sql )
274 game = cursor.fetchone()
275
276 self.dbGameID = gameID
277
278 self.teamName [ "1" ], game[ "t1name" ] )
279 self.teamName ( "2" , game[ "t2name" ] )
280
281 @cherrypy.expose
282 def teamName( self , team , name ):
283 if team == "1": self.scoreboard.scoreA.label = name
284 if team == "2": self.scoreboard.scoreB.label = name
285
286 @cherrypy.expose
287 def score( self, team1, team2 ):
288 self.scoreboard.scoreA.value += int( team1 )
289 self.scoreboard.scoreB.value += int( team2 )
290
291 if team1 != "0": self.gameEvent( "T1SCORE", team1 )
292 if team2 != "0": self.gameEvent( "T2SCORE", team2 )
293
294 self.scoreboard.render()
295 return str( self.scoreboard.scoreA.value + ":" +
 str( self.scoreboard.scoreB.value ) )
296
297 @cherrypy.expose
298 def timeout2( self, team1, team2 ):
299 self.scoreboard.timeoutA.value += int( team1 )
300 self.scoreboard.timeoutB.value += int( team2 )
301
302 if team1 != "0": self.gameEvent( "T1TIMEOUT", team1 )
303 if team2 != "0": self.gameEvent( "T2TIMEOUT", team2 )
304
305 return str( self.scoreboard.timeoutA.value ) + ":" +
 str( self.scoreboard.timeoutB.value )
306
307 @cherrypy.expose
308 def period( self, period ):
309 self.gameEvent( "PERIOD", period )
310
311 self.scoreboard.period.value += int( period )
312 return str( self.scoreboard.period.value )
313
314 @cherrypy.expose
315 def getClock( self ):
316 return self.scoreboard.clk.clockString
317
318 @cherrypy.expose
319 def clockRun( self ):
320 self.scoreboard.clk.running = True
321
```

```
322 @cherrypy.expose
323 def clockStop( self ):
324 self.scoreboard.clk.running = False
325 self.gameEvent( "CLOCKSTOP", 0 )
326
327 @cherrypy.expose
328 def clockSet( self , seconds ):
329 self.scoreboard.clk.seconds = int( seconds ) + 1
330 self.scoreboard.clk.tick ( manual = True )
331 return self.scoreboard.clk.clockString
332
333 @cherrypy.expose
334 def possession( self ):
335 self.scoreboard.possession.toggle()
336 if self.scoreboard.possession.leftString == "<":
 self.gameEvent( "POSSESSION", 1 )
337 if self.scoreboard.possession.rightString == ">":
 self.gameEvent( "POSSESSION", 2 )
338
339 return self.scoreboard.possession.leftString + ":" +
 self.scoreboard.possession.rightString
340
341 class clock:
342 def __init__( self , screen ):
343 self.screen = screen
344 self.width = self.screen.get_width()
345 self.height = 250
346 self.seconds = 6 \* 60
347 self.clockSurf = pygame.surface.Surface( (
 self.width , self.height ) )
348 self.clockFont = pygame.font.Font( "Open24.ttf" ,
 self.height )
349 self.running = False
350
351 mins = int( float( self.seconds ) / 60.0 )
352 secs = self.seconds % 60
353
354 self.clockString = "{0}:{1:02d}".format( mins ,
 secs )
355
356 def tick( self , manual = False ):
357 if self.seconds > 0 and( self.running = True or
 manual = True ):
358 self.seconds -\- 1
359
360 mins = int( float( self.seconds ) / 60.0 )
361 secs = self.seconds % 60
362
363 self.clockString = "{0}:{1:02d}".format( mins , secs )
364
365 def render( self ):
366 timeSurf = self.clockFont.render( self.clockString ,
 True, ( 0 , 255 , 0 ) )
367
368 x = self.width / 2 - int( timeSurf.get_width() / 2 )
369 self.clockSurf.fill( ( 0 , 0 , 0 ) )
370 self.clockSurf.blit( timeSurf, ( x, -28 ) )
371 return self.clockSurf
```