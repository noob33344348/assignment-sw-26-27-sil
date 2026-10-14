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

## Tests

### test_smu_plausiblity
<p>It's the same as test_smu_fault, but the APP2 is artificially set to 3300. So that it differs by more then 50 counts, and around 30%</p>

### test_smu_periodic_output
<p>Reusing wait_for_frame, it checks that smu publishes n frames in time.</p>
<p>Warning: wait_for_frame has a timeout of 300ms, this is applied for any value of n.</p>
<p>If this test needs to check with more granularity a solution could be implementing wait_for_frame that also includes a parameter for a different timeout.</p>

### test_ebs_missing_input
<p>Restarting the system after every possible missing frame to correctly separate the 3 cases.</p>

### test_ebs_pressure_fault
<p>Restarting the system after every possible missing frame to correctly separate the 3 cases.</p>
<p>Sending correct nominal values before the faulty one to establish known good baseline.</p>

## CI Workflow
<p> --fresh additionally requests a fresh build-tree configuration. </p>
