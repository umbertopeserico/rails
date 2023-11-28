*   Remove deprecated support to pass `deferrable: true` to `add_foreign_key`.

    *Rafael Mendonça França*

*   Remove deprecated support to quote `ActiveSupport::Duration`.

    *Rafael Mendonça França*

*   Remove deprecated `#quote_bound_value`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::ConnectionAdapters::ConnectionPool#connection_klass`.

    *Rafael Mendonça França*

*   Remove deprecated support to apply `#connection_pool_list`, `#active_connections?`, `#clear_active_connections!`,
    `#clear_reloadable_connections!`, `#clear_all_connections!` and `#flush_idle_connections!` to the connections pools
    for the current role when the `role` argument isn't provided.

    *Rafael Mendonça França*

*   Remove deprecated `#all_connection_pools`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::ConnectionAdapters::SchemaCache#data_sources`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::ConnectionAdapters::SchemaCache.load_from`.

    *Rafael Mendonça França*

*   Remove deprecated `#all_foreign_keys_valid?` from database adapters.

    *Rafael Mendonça França*

*   Remove deprecated support to passing coder and class as second argument to `serialize`.

    *Rafael Mendonça França*

*   Remove deprecated support to `ActiveRecord::Base#read_attribute(:id)` to return the custom primary key value.

    *Rafael Mendonça França*

*   Remove deprecated `TestFixtures.fixture_path`.

    *Rafael Mendonça França*

*   Remove deprecated behavior to support referring to a singular association by its plural name.

    *Rafael Mendonça França*

*   Deprecate `Rails.application.config.active_record.allow_deprecated_singular_associations_name`

    *Rafael Mendonça França*

*   Remove deprecated support to passing `SchemaMigration` and `InternalMetadata` classes as arguments to
    `ActiveRecord::MigrationContext`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::Migration.check_pending` method.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::LogSubscriber.runtime` method.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::LogSubscriber.runtime=` method.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::LogSubscriber.reset_runtime` method.

    *Rafael Mendonça França*

*   Remove deprecated support to define `explain` in the connection adapter with 2 arguments.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::ActiveJobRequiredError`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::Base.clear_active_connections!`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::Base.clear_reloadable_connections!`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::Base.clear_all_connections!`.

    *Rafael Mendonça França*

*   Remove deprecated `ActiveRecord::Base.flush_idle_connections!`.

    *Rafael Mendonça França*

*   Remove deprecated `name` argument from `ActiveRecord::Base.remove_connection`.

    *Rafael Mendonça França*

*   Remove deprecated support to call `alias_attribute` with non-existent attribute names.

    *Rafael Mendonça França*

*   Remove deprecated `Rails.application.config.active_record.suppress_multiple_database_warning`.

    *Rafael Mendonça França*

*   In cases where MySQL returns `warning_count` greater than zero, but returns no warnings when
    the `SHOW WARNINGS` query is executed, `ActiveRecord.db_warnings_action` proc will still be
    called with a generic warning message rather than silently ignoring the warning(s).

    *Kevin McPhillips*

*   `DatabaseConfigurations#configs_for` can accept a symbol in the `name` parameter.

    *Andrew Novoselac*

*   Fix `where(field: values)` queries when `field` is a serialized attribute
    (for example, when `field` uses `ActiveRecord::Base.serialize` or is a JSON
    column).

    *João Alves*

*   Make the output of `ActiveRecord::Core#inspect` configurable.

    By default, calling `inspect` on a record will yield a formatted string including just the `id`.

    ```ruby
    Post.first.inspect #=> "#<Post id: 1>"
    ```

    The attributes to be included in the output of `inspect` can be configured with
    `ActiveRecord::Core#attributes_for_inspect`.

    ```ruby
    Post.attributes_for_inspect = [:id, :title]
    Post.first.inspect #=> "#<Post id: 1, title: "Hello, World!">"
    ```

    With the `attributes_for_inspect` set to `:all`, `inspect` will list all the record's attributes.

    ```ruby
    Post.attributes_for_inspect = :all
    Post.first.inspect #=> "#<Post id: 1, title: "Hello, World!", published_at: "2023-10-23 14:28:11 +0000">"
    ```

    In development and test mode, `attributes_for_inspect` will be set to `:all` by default.

    You can also call `full_inspect` to get an inspection with all the attributes.

    The attributes in `attribute_for_inspect` will also be used for `pretty_print`.

    *Andrew Novoselac*

*   Don't mark Float::INFINITY as changed when reassigning it

    When saving a record with a float infinite value, it shouldn't mark as changed

    *Maicol Bentancor*

*   Support `RETURNING` clause for MariaDB

    *fatkodima*, *Nikolay Kondratyev*

*   The SQLite3 adapter now implements the `supports_deferrable_constraints?` contract

    Allows foreign keys to be deferred by adding the `:deferrable` key to the `foreign_key` options.

    ```ruby
    add_reference :person, :alias, foreign_key: { deferrable: :deferred }
    add_reference :alias, :person, foreign_key: { deferrable: :deferred }
    ```

    *Stephen Margheim*

*   Add `set_constraints` helper for PostgreSQL

    ```ruby
    Post.create!(user_id: -1) # => ActiveRecord::InvalidForeignKey

    Post.transaction do
      Post.connection.set_constraints(:deferred)
      p = Post.create!(user_id: -1)
      u = User.create!
      p.user = u
      p.save!
    end
    ```

    *Cody Cutrer*

*   Include `ActiveModel::API` in `ActiveRecord::Base`

    *Sean Doyle*

*   Ensure `#signed_id` outputs `url_safe` strings.

    *Jason Meller*

Please check [7-1-stable](https://github.com/rails/rails/blob/7-1-stable/activerecord/CHANGELOG.md) for previous changes.
