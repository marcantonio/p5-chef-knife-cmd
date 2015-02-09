# NAME

Chef::Knife::Cmd - A small wrapper around the Chef 'knife' command line utility

# SYNOPSIS

    use Chef::Knife::Cmd;

    my $knife = Chef::Knife::Cmd->new(
        verbose   => 1,           # tee output to STDOUT
        logfile   => 'knife.log', # all cmd output logged here
        print_cmd => 1,           # if you want knife cmd printed to STDOUT
    );

    # knife bootstrap
    $knife->bootstrap($fqdn, %options);

    # knife client
    $knife->client->delete($client, %options);

    # knife ec2
    $knife->ec2->server->list(%options);
    $knife->ec2->server->create(%options);
    $knife->ec2->server->delete(\@nodes, %options);

    # knife node
    $knife->node->show($node, %options);
    $knife->node->list($node, %options);
    $knife->node->create($node, %options);
    $knife->node->delete($node, %options);
    $knife->node->flip($node, $environment, %options);
    $knife->node->run_list->add($node, \@entries, %options);

    # knife vault commands
    # hint: use $knife->vault->item() instead of $knife->vault->show()
    $knife->vault->create($vault, $item, $values, %options);
    $knife->vault->update($vault, $item, $values, %options);
    $knife->vault->show($vault, $item_name, %options);
    my $item = $knife->vault->item($vault, $item_name, %options);
    say $item->{secret};
    say $item->{super_secret};

# DESCRIPTION

This module is a small wrapper around the Chef 'knife' command line utility.

It would be awesome if this module used the Chef server API, but this module is
not that awesome.

Some things to know about this module:

- Return vaules

    All commands return the output of the knife command.  

- Logging

    All knife cmd output is logged to a logfile for later analysis.  This allows
    you to provide verbose logging to users while not cluttering their terminal
    with tons of output.

- Tee output to STDOUT

    Instead of waiting for an hour for a knife command to finish, you can view
    output from the knife command in real time as it happens.  This happens when
    the 'verbose' attribute is true.

- Exceptions

    If a knife command fails, this module will throw an exception.

- No need to mess about with string manipulation

    Yay.

# SEE ALSO

- Capture::Tiny::Extended
- Capture::Tiny
- IPC::System::Simple

# ABOUT THE NAME

I didn't name this Chef::Knife because I'm hoping someone someday will write a
real Chef::Knife module which uses the Chef server API.

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# AUTHOR

Eric Johnson <eric.git@iijo.org>