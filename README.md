Lab 2: UDP File Transfer Upgrade
----
Anupa Ragoonanan (n01423202)

CPAN 225 RNA

February 6, 2026

----

Screenshot 1: The two jpg files (old_lady.jpg and the received version) from the direct client to server transfer 
(without the relay).

![RagoonananAnupa_Lab2](https://github.com/user-attachments/assets/f62685e7-93c3-4fdd-b4ae-0db528150689)

----

Screenshot 2: The corrupted received_relay.jpg (from Test B).

![RagoonananAnupa_Lab2(2)](https://github.com/user-attachments/assets/c7d98fdc-c752-4abd-8c12-09a8a18c1f79)

----

Screenshot 3: The clean received.jpg after your code fix, successfully transferred through the relay.

![RagoonananAnupa_Lab2(3)](https://github.com/user-attachments/assets/cc82a8b9-7f0e-4bad-9c6c-f127143cb52c)

----

Screenshot 4: The result of the Final check.

![RagoonananAnupa_Lab2_FinalCheck](https://github.com/user-attachments/assets/72da20b9-fa23-4e95-af10-34c31a6604d0)

----

How does Buffer logic work?

The buffer logic uses an ordered dictionary to manage out-of-order packet arrival. The server tracks which packet 
it expects next, beginning from zero. If a packet arrives with the expected sequence number, its data is saved and 
the server moves on to wait for the next number. If a packet arrives too early—with a higher sequence number than 
expected—the server stores its data in the buffer, keyed by that sequence number. Once the expected packet is 
received and processed, the server repeatedly checks the buffer for the next consecutive packet. If it finds it, 
the server removes that buffered data, appends it to the file, and continues checking for the following number in 
sequence. This process ensures the file is reconstructed in the correct order even when packets are delivered out 
of sequence.
