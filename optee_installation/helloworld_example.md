
## How to Run the Example
To execute the Hello World example on an OP-TEE enabled Raspberry Pi, use the following command in the terminal:


`optee_example_hello_world`

## Example's Purpose
This OP-TEE Hello World example showcases the interaction between a non-secure world client application and a secure world Trusted Application (TA).

## Execution Flow
- **Initialization**: The non-secure world client begins by initializing a context with the TEE.
- **TA Loading**: The Hello World TA is loaded by the OP-TEE OS into the secure world.
- **Session Opening**: A session from the non-secure world client to the secure world TA is opened.
- **Command Invocation**: The client invokes a command on the TA to perform an operation.
- **Output**: The TA executes and outputs "Hello World!".
- **Increment Operation**: The TA receives a value of 42, increments it, and returns the new value (43) to the client.
- **Session Closure**: The client application closes the session, releasing any allocated resources.
- **TA Destruction**: The TA is destroyed, which unloads it from the secure world memory.

## Output
```bash
$ optee_example_hello_world 
D/TC:? 0 tee_ta_init_pseudo_ta_session:297 Lookup pseudo TA 8aaaf200-2450-11e4-abe2-0002a5d5c51b
D/TC:? 0 ldelf_load_ldelf:110 ldelf load address 0x40007000
D/LD:  ldelf:142 Loading TS 8aaaf200-2450-11e4-abe2-0002a5d5c51b
D/TC:? 0 ldelf_syscall_open_bin:163 Lookup user TA ELF 8aaaf200-2450-11e4-abe2-0002a5d5c51b (early TA)
D/TC:? 0 ldelf_syscall_open_bin:167 res=0xffff0008
D/TC:? 0 ldelf_syscall_open_bin:163 Lookup user TA ELF 8aaaf200-2450-11e4-abe2-0002a5d5c51b (Secure Storage TA)
I/TC: WARNING (insecure configuration): Failed to get monotonic counter for REE FS, using 0
D/TC:? 0 ldelf_syscall_open_bin:167 res=0xffff0008
D/TC:? 0 ldelf_syscall_open_bin:163 Lookup user TA ELF 8aaaf200-2450-11e4-abe2-0002a5d5c51b (REE)
D/TC:? 0 ldelf_syscall_open_bin:167 res=0
I/TC: WARNING (insecure configuration): Failed to commit dirh counter 909
D/LD:  ldelf:176 ELF (8aaaf200-2450-11e4-abe2-0002a5d5c51b) at 0x40051000
D/TA:  TA_CreateEntryPoint:39 has been called
D/TA:  __GP11_TA_OpenSessionEntryPoint:68 has been called
I/TA: Hello World!
InvokingD/TA:  inc_value:105 has been called
 TA to iI/TA: Got value: 42 from NW
ncrementI/TA: Increase value to: 43
 42
D/TC:? 0 tee_ta_close_session:468 csess 0x10195f30 id 1
TA increD/TC:? 0 tee_ta_close_session:487 Destroy session
mented vI/TA: Goodbye!
alue to D/TA:  TA_DestroyEntryPoint:50 has been called
43
D/TC:? 0 destroy_context:326 Destroy TA ctx (0x10195ed0)
```
## Explanation of Each Line
- **`D/TC:? 0 tee_ta_init_pseudo_ta_session:`**: Debug log from OP-TEE OS initializing a session with a pseudo-TA.
- **`D/LD:  ldelf:`**: Debug logs from the OP-TEE OS secure loader.
- **`D/TC:? 0 tee_ta_invoke_command:`**: Debug log indicating the invocation of a command on the TA.
- **`I/TA: Hello World!`**: The TA's standard output, printing "Hello World!".
- **`D/TC:? 0 tee_ta_close_session:`**: Debug log indicating the closing of the TA session.
- **`D/TC:? 0 destroy_context:`**: Debug log for the destruction of the context associated with the TA.

## Warnings and Their Meaning
- **`WARNING: 'Insecure configuration'`**: This warning indicates that the system may not be fully secure, which could be due to a non-production configuration or because certain security features are disabled for development/testing.
- **`WARNING: 'Failed to get monotonic counter'`**: This warning signals a failure to retrieve a secure time source, which may affect time-based operations in the secure world. This could occur due to missing support in a development environment.

These warnings are typical in a development setup and indicate that the system is not configured for a secure production deployment.
```
