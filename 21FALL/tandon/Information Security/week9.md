# Vituralize
    isolate
    limate the scope of damage
    developer doesn't need to know details about how vituralization workes
    damage like buffer overflow

    resource isolation
    
    fork bomb
        why can't kill the root process
        have to call the kill process, but there is no space for the command.

    filling memory
        apt package manager-  keep downloading to the memory-> slow the system
    filling disk
        yum package manager
    easy for one process to bring down a system
        SSL- client kepp request , the server keep decrypt it
    OS as A reference Monitor
    
    Translation Lookaside Buffer
        Maps virtual to physical addresses
        located next to the cache
    
    TLB hit/ TLB miss
        miss -> raises a page fault exception -> os catch the exception, and brings the missing page to the memeory
        expensive conext switch

    Modern Hardware
        more registers big memeory pages.
        principle of least privilege -> each process should live in its own address

    Level:
        Data isolate 
        Fault isolate
        Performance
        No assumptions required for software inside a VM

    VM type:
        type1   native bare-metal  没有操作系统的计算机硬件 more secure , doesn't worry about hosts' security.
        type2   hosted  

        type1   run upper mainframe -> hypervisor: manage hardware resources.
                IBM VM: hardware is so expensive, so separate it.

        type1a  vm is application environment
        type1b  linux
        type2   vmware workstation
                high overhead vm
                workstation is an applicationthat hosts Oss.
        
    Contains:   lightweight OS-like system 
                Each app in its own container
    
    Programming Language VM:
    Trusted Code in Sandbox
    Trusted Computing Base(TCB)
        any failure is fatal
        privilege is widely used
    Traditional Policy Interpositon
        Function is scattered 
    
    Process safe
        Memory safe
        Control-flow safety
        Type safety 
    Software fault Isolation (SFI)
    Fault Domain:   
    Verifying Jumps and Stores
    