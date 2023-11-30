
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
1. **Command Execution**:
   ```
   $ optee_example_hello_world
   ```
   - Executes the Hello World program in OP-TEE.

2. **Session Initialization with Pseudo TA**:
   ```
   D/TC:? 0 tee_ta_init_pseudo_ta_session:297 Lookup pseudo TA 8aaaf200-2450-11e4-abe2-0002a5d5c51b
   ```
   - Initiates a session with a pseudo Trusted Application (TA) identified by a specific UUID.

3. **ldelf Loading**:
   ```
   D/TC:? 0 ldelf_load_ldelf:110 ldelf load address 0x40007000
   ```
   - The ldelf (secure loader) component is loaded into a specific memory address.

4. **Loading TS with UUID**:
   ```
   D/LD: ldelf:142 Loading TS 8aaaf200-2450-11e4-abe2-0002a5d5c51b
   ```
   - The Trusted Service with the given UUID is being loaded.

5. **Lookup of TA ELF Binary**:
   ```
   D/TC:? 0 ldelf_syscall_open_bin:163 Lookup user TA ELF (various types)
   ```
   - Several attempts to locate the TA's ELF binary across different storage types (early TA, Secure Storage, REE).

6. **Configuration Warnings**:
   ```
   I/TC: WARNING (insecure configuration)
   ```
   - Indicates potential configuration issues, like an insecure setup.

7. **ELF File Loading**:
   ```
   D/LD: ldelf:176 ELF at a specific memory address
   ```
   - The ELF file of the TA is loaded into memory.

8. **TA Creation and Session Opening**:
   ```
   D/TA: TA_CreateEntryPoint and __GP11_TA_OpenSessionEntryPoint
   ```
   - Indicates the creation of the TA and the opening of a session with it.

9. **TA Output and Operations**:
   ```
   I/TA: Hello World!, Got value: 42, Increase value to: 43
   ```
   - The TA prints "Hello World!", receives and increments a value.

10. **Session Closure and TA Destruction**:
   ```
   D/TC:? 0 tee_ta_close_session and TA_DestroyEntryPoint
   ```
   - The session is closed, and the TA is destroyed, including output like "Goodbye!".

These lines provide a comprehensive view of the initialization, execution, and termination processes within a TEE using OP-TEE, demonstrating typical interactions with a Trusted Application.

### In the output of `optee_example_hello_world`, the following prefixes are observed along with their meanings:

- **`D/TC`**: "Debug/Trusted Core" - These messages are debug logs from the Trusted Core component of OP-TEE, which is responsible for secure world operations.

- **`D/LD`**: "Debug/Loader" - These are debug messages from the loader component in OP-TEE, related to loading and handling of Trusted Applications.

- **`I/TC`**: "Information/Trusted Core" - Informational messages from the Trusted Core. The messages marked with this prefix often include warnings or general information about the system's state.

- **`D/TA`**: "Debug/Trusted Application" - Debug messages specific to the Trusted Application's operations and lifecycle events.

- **`I/TA`**: "Information/Trusted Application" - Informational messages or output from the Trusted Application.

## Warnings and Their Meaning
- **`WARNING: 'Insecure configuration'`**: This warning indicates that the system may not be fully secure, which could be due to a non-production configuration or because certain security features are disabled for development/testing.
- **`WARNING: 'Failed to get monotonic counter'`**: This warning signals a failure to retrieve a secure time source, which may affect time-based operations in the secure world. This could occur due to missing support in a development environment.

These warnings are typical in a development setup and indicate that the system is not configured for a secure production deployment.
```
