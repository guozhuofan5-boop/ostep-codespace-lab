## Q1
- Prediction / 预测:Total Time = 10, CPU Busy = 10 (100%), I/O Busy = 0 (0%)
- Reasoning / 理由: Both processes require only CPU execution and do not perform any I/O operations. The CPU therefore remains busy throughout the entire execution. PID 0 uses 5 ticks, and PID 1 uses another 5 ticks. Thus, the total time is 10 ticks, with 100% CPU utilization and 0% I/O utilization. / 两个进程都只需要使用 CPU，不涉及任何 I/O 操作，因此 CPU 在整个执行过程中始终处于忙碌状态。PID 0 执行 5 个 tick，PID 1 随后执行另外 5 个 tick。因此，总时间为 10 个 tick，CPU 利用率为 100%，I/O 利用率为 0%。
- Verified result / 验证结果: 
- Analysis / 分析: 

## Q2
- Prediction / 预测:Total Time = 11, CPU Busy = 6 (54.55%), I/O Busy = 5 (45.45%)
- Reasoning / 理由:PID 0 executes its 4 CPU instructions first, taking 4 ticks. After that, PID 1 begins its I/O operation, spending 1 tick to issue the request and 5 ticks waiting while the device processes it. Once the I/O operation finishes, PID 1 uses 1 additional tick to handle the completion. Because PID 0 has already finished, the CPU remains idle while PID 1 is blocked. Therefore, the total time is 11 ticks, with 6 ticks of CPU activity and 5 ticks of I/O activity./PID 0 首先执行 4 条 CPU 指令，共花费 4 个 tick。随后，PID 1 开始执行 I/O 操作，花费 1 个 tick 发出请求，并等待设备处理 5 个 tick。I/O 操作完成后，PID 1 还需要 1 个 tick 来处理完成事件。由于 PID 0 已经执行结束，当 PID 1 处于阻塞状态时，CPU 没有其他进程可以执行，因此会处于空闲状态。最终，总时间为 11 个 tick，其中 CPU 忙碌 6 个 tick，I/O 忙碌 5 个 tick。
- Verified result / 验证结果: 
- Analysis / 分析: 

## Q3
- Prediction / 预测: Total Time = 7, CPU Busy = 6 (85.71%), I/O Busy = 5 (71.43%)
- Reasoning / 理由:PID 0 starts the I/O operation during tick 1. Since the scheduling policy is set to SWITCH_ON_IO, the CPU switches to PID 1 while PID 0 waits for the I/O operation to finish. During ticks 2–5, PID 1 executes its 4 CPU instructions. At tick 6, the CPU becomes idle because PID 1 has finished while PID 0 is still waiting for I/O completion. PID 0 then handles the I/O completion in tick 7. As a result, the total execution time is 7 ticks, with 6 ticks of CPU activity and 5 ticks of I/O activity./PID 0 在第 1 个 tick 发起 I/O 操作。由于调度策略为 SWITCH_ON_IO，CPU 随后切换到 PID 1，让 PID 0 等待 I/O 操作完成。在第 2 至第 5 个 tick 期间，PID 1 执行完 4 条 CPU 指令。到了第 6 个 tick，PID 1 已经执行结束，而 PID 0 的 I/O 操作仍未完成，因此 CPU 暂时空闲。第 7 个 tick，PID 0 处理 I/O 完成事件。最终，总执行时间为 7 个 tick，CPU 忙碌时间为 6 个 tick，I/O 忙碌时间为 5 个 tick。
- Verified result / 验证结果:
- Analysis / 分析:

## Q4
- Prediction / 预测:Total Time = 11, CPU Busy = 6 (54.55%), I/O Busy = 5 (45.45%)
- Reasoning / 理由: When using the SWITCH_ON_END policy, the CPU does not switch to another process until the current process has completely finished. PID 0 initiates I/O and remains blocked for 5 ticks (ticks 2–6), during which the CPU stays idle because PID 1 cannot run yet. After PID 0 completes its I/O handling at tick 7, PID 1 begins executing its 4 CPU instructions from ticks 8–11. Therefore, the total execution time is 11 ticks, with 6 ticks of CPU activity and 5 ticks of I/O activity./在 SWITCH_ON_END 调度策略下，当前进程完全结束之前，CPU 不会切换到其他进程。PID 0 发起 I/O 操作后，会阻塞 5 个 tick（第 2 至第 6 个 tick）。在此期间，由于 PID 1 还不能运行，CPU 只能保持空闲。PID 0 在第 7 个 tick 完成 I/O 处理后，PID 1 才开始执行自己的 4 条 CPU 指令，运行时间为第 8 至第 11 个 tick。因此，总执行时间为 11 个 tick，其中 CPU 忙碌 6 个 tick，I/O 忙碌 5 个 tick。
- Verified result / 验证结果: 
- Analysis / 分析:

## Q5
- Prediction / 预测: Total Time = 7, CPU Busy = 6 (85.71%), I/O Busy = 5 (71.43%)
- Reasoning / 理由: The process configuration is identical to Q3, and the SWITCH_ON_IO policy is explicitly enabled. When PID 0 initiates an I/O operation, the CPU immediately switches to PID 1, allowing it to execute its 4 CPU instructions while PID 0 is waiting. After PID 1 finishes, the CPU remains idle for 1 tick until PID 0's I/O operation completes. PID 0 then handles the completion event in the final tick. Therefore, the total execution time is 7 ticks, with 6 ticks of CPU activity and 5 ticks of I/O activity, producing the same result as Q3./本题的进程配置与 Q3 相同，并且明确设置了 SWITCH_ON_IO 调度策略。当 PID 0 发起 I/O 操作后，CPU 会立即切换到 PID 1，使其能够在 PID 0 等待期间执行 4 条 CPU 指令。PID 1 执行结束后，由于 PID 0 的 I/O 操作尚未完成，CPU 会空闲 1 个 tick。最后，PID 0 在最后一个 tick 处理 I/O 完成事件。因此，总执行时间为 7 个 tick，CPU 忙碌时间为 6 个 tick，I/O 忙碌时间为 5 个 tick，结果与 Q3 相同。
- Verified result / 验证结果: 
- Analysis / 分析: 

## Q6
- Prediction / 预测: With the -I IO_RUN_LATER option enabled, PID 0 is expected to finish later than the CPU-bound processes, even though it has fewer instructions to execute.启用 -I IO_RUN_LATER 选项后，尽管 PID 0 需要执行的指令较少，但它预计会比纯 CPU 密集型进程更晚完成。
- Reasoning / 理由: PID 0 initiates an I/O operation and switches to another process under the SWITCH_ON_IO policy. While PID 0 is blocked, the other processes continue using the CPU. With IO_RUN_LATER, PID 0 is placed at the end of the ready queue when its I/O operation completes, rather than immediately resuming execution. This happens repeatedly for each of its 3 I/O operations, potentially delaying its completion until after the CPU-bound processes have finished./PID 0 发起 I/O 操作后，会根据 SWITCH_ON_IO 策略切换到其他进程执行。在 PID 0 被阻塞期间，其他进程继续使用 CPU。由于启用了 IO_RUN_LATER，每当 PID 0 的 I/O 操作完成时，它都会被放到就绪队列的末尾，而不是立即恢复执行。这个过程会在它的 3 次 I/O 操作中重复发生，因此 PID 0 的完成时间可能会不断推迟，甚至晚于纯 CPU 密集型进程。
- Verified result / 验证结果: 
- Analysis / 分析: 

## Q7
- Prediction / 预测: With IO_RUN_IMMEDIATE enabled, PID 0 can resume execution immediately after each I/O operation completes, allowing it to issue its next I/O request sooner. This should reduce delays and potentially shorten the total execution time compared with Q6./启用 IO_RUN_IMMEDIATE 后，每次 I/O 操作完成时，PID 0 都可以立即恢复执行，从而更快地发起下一次 I/O 请求。这有助于减少等待时间，并可能缩短总执行时间，相比 Q6 更快完成。
- Reasoning / 理由: Unlike IO_RUN_LATER in Q6, which places PID 0 at the end of the ready queue after each I/O completion, IO_RUN_IMMEDIATE allows PID 0 to return to the CPU immediately. This enables it to issue its next I/O request without waiting behind other CPU-bound processes. As a result, PID 0's three I/O operations can occur closer together, potentially improving I/O device utilization and reducing the overall completion time./与 Q6 中的 IO_RUN_LATER 不同，后者会在每次 I/O 完成后将 PID 0 放到就绪队列末尾，而 IO_RUN_IMMEDIATE 允许 PID 0 立即返回 CPU 执行。因此，它不必排在其他 CPU 密集型进程后面等待，就能更快地发起下一次 I/O 请求。这样，PID 0 的三次 I/O 操作可以更加紧凑地进行，从而有望提高 I/O 设备的利用率，并缩短整体执行时间。
- Verified result / 验证结果: 
- Analysis / 分析: 

## Q8
- Prediction / 预测: Because the instruction sequences are generated based on the random seed, the exact results are difficult to determine in advance. However, SWITCH_ON_END is expected to perform worse than the default scheduling policy (IO_RUN_IMMEDIATE) because it prevents other processes from running while the current process is waiting for I/O./由于进程的指令序列由随机种子决定，因此很难提前准确预测具体结果。不过，与默认调度策略 IO_RUN_IMMEDIATE 相比，SWITCH_ON_END 的表现预计会更差，因为当前进程等待 I/O 时，其他进程无法运行，导致 CPU 不能充分利用等待时间。
- Reasoning / 理由:With seed 1, PID 0 executes one CPU instruction followed by two I/O instructions, while PID 1 executes three CPU instructions. Under the default IO_RUN_IMMEDIATE policy, PID 1 can run while PID 0 waits for its first I/O operation. However, PID 1 finishes at tick 6, before PID 0's I/O completes at tick 8. Since no other process is waiting to use the CPU, IO_RUN_LATER and IO_RUN_IMMEDIATE produce the same result in this case. In contrast, under SWITCH_ON_END, PID 1 cannot start until PID 0 has completely finished, preventing the two processes from overlapping their execution and I/O waiting periods./在随机种子为 1 时，PID 0 的指令序列为一条 CPU 指令和两条 I/O 指令，而 PID 1 则执行三条 CPU 指令。在默认的 IO_RUN_IMMEDIATE 策略下，PID 0 等待第一次 I/O 操作期间，PID 1 可以使用 CPU 执行任务。不过，PID 1 在第 6 个 tick 就已经结束，而 PID 0 的 I/O 操作要到第 8 个 tick 才完成。由于此时没有其他进程需要竞争 CPU，因此在这个例子中，IO_RUN_LATER 和 IO_RUN_IMMEDIATE 的执行结果相同。相比之下，在 SWITCH_ON_END 策略下，PID 1 必须等到 PID 0 完全结束后才能运行，无法让两个进程的执行过程与 I/O 等待时间重叠。
- Verified result / 验证结果: 
- Analysis / 分析: