page wraps around to the first. Two hands sweep through the physical page list, as shown in Figure 5.22.

![](bbox=[0.354, 0.186, 0.65, 0.343])

**Figure 5.22** *Two-Handed Clock Algorithm*

The two hands, the front hand and back hand, rotate clockwise in page order around the list. The front hand rotates ahead of the back hand, clearing the referenced and modified bits for each page. The trailing back hand then inspects the referenced and modified bits some time later. Pages that have not been referenced or modified are swapped out and freed. The rate at which the hands rotate around the page list is controlled by the amount of free memory on the system, and the gap between the front hand and back hand is fixed by a boot-time parameter, handspreadpages.

# 5.8.2 Page-out Algorithm and Parameters

The page-out algorithm is controlled by several parameters, some of which are calculated at system startup by the amount of memory in the system, and some of which are calculated dynamically based on memory allocation and paging activity.

The parameters that control the clock hands do two things: they control the rate at which the scanner scans through pages, and they control the time (or distance) between the front hand and the back hand. The distance between the back hand and the front hand is handspreadpages and is expressed in units of pages. The maximum distance between the front hand and back hand defaults to half of memory and is capped at 8,192 pages, or 64 Mbytes. Systems with 128 Mbytes or more of memory always default this distance to 8,192 pages, or 64 Mbytes.

# 5.8.2.1 Scan Rate Parameters (Assuming No Priority Paging)

The scanner starts scanning when free memory is lower than lotsfree number of pages free plus a small buffer factor, deficit. The scanner starts scanning at a rate of slowscan pages per second at this point and gets faster as the amount of free memory approaches zero. The system parameter lotsfree is calculated at startup as 1/64th of memory, and the parameter deficit is either zero or a small number of pages—set by the page allocator at times of large memory allocation to