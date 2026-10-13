# Thought Process

## thread-safety and local bus

### mutex
<p>I used only the provided mutex for protecting state variables.</p>
<p>Using the same mutex to protect different variables may cause locks when non needed.</p>
<p>A solution is using different mutex, one for each variable to protect, and simply lock accordingly.</p>

### SilSystem::try_read
<p>I think the request implied to save the popped Frame,
else the frame parameter is useless and should be removed.</p>


### SilSystem::write

<p>I think the request implied to remove the oldest frame to keep the queues bounded by kQueueCapacity.</p>

<p>From my undestanding only one thread uses emitted_avaible,
so notify_one should be more appropriate then notify_all.<p>

### SilSystem::write_output

<p>I have not understood the meaning of have the ecu parameter.</p>

## CI Workflow
<p> --fresh additionally requests a fresh build-tree configuration. </p>
