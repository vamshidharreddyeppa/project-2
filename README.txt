# Project 2 - Diagnose the Failure Twice

Tier targeted: Normal

Incident diagnosed:
Ollama was killed by the Linux OOM killer.

Root cause verified:
The Ollama process loaded deepseek-7b FP16 with a large KV cache, and the machine did not have enough memory for that workload.

Offending line:
Jun 19 02:31:09 relief-gpu kernel: Out of memory: Killed process 8423 (ollama) total-vm:18402112kB, anon-rss:15994208kB, file-rss:0kB, shmem-rss:0kB, UID:1000 oom_score_adj:0

Artifacts:
1. evidence/sample-incident.log
2. evidence/sample-dmesg.log
3. evidence/sample-ps.txt
4. HAND_DIAGNOSIS.txt
5. ai-transcript.txt
6. ADJUDICATION.txt
7. REPORT.docx

Where the AI helped:
The AI helped confirm that the issue was memory related and that the OOM killer killed the Ollama process.

Where the AI lied or went wrong:
The AI did not fully quote the offending log line exactly. It shortened the line by removing the timestamp, hostname, and kernel prefix.

Verified fix:
Use a smaller or quantized model such as Q4_K_M, reduce the context and batch size, or upgrade the machine memory.

What I learned:
I learned that the first diagnosis should come from the raw evidence before asking AI. The AI was useful, but it still needed checking against the actual log files.

AI usage:
Model used: gemini-3.1-flash-lite. Used for the second diagnosis after my hand diagnosis was already written.

Signed: Vamshidhar Reddy Eppa
