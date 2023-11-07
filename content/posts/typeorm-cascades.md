---
title: '💡 TypeORM Cascades'
description: A brief overview of cascades in TypeORM.
date: 2023-11-07
publishDate: 2023-11-07
tags: [TypeORM, TypeScript, Database]
showReadingTime: true
showToc: false
tocOpen: false
---

## Cascades

There are two types of "cascades" in [TypeORM](typeorm). First, we have _database cascades_.

### Database Cascades

This is probably what you have heard of and are familiar with. It is the standard _when a parent is deleted, also delete the children_. These are super convenient when you have linked data and you want to automatically perform some action when a delete happens. Instead of manually deleting linked records before the deleting the target row, you can delegate this responsibility to the database through cascades. It is also worth noting that `CASCADE` is not the only action that can be taken. You can also use any of the following actions:

- `CASCADE` - cascade the update/delete
- `NO ACTION` - do nothing
- `SET NULL` - set the column to `null`
- `SET DEFAULT` - set the column its default value

While `ON DELETE` is probably the most common (and useful), there are actually two events that I normally set `ON DELETE` and `ON UPDATE`.

- `ON DELETE` is what I described above, cascade the _delete_ event to the children, also deleting them.
- `ON UPDATE` is when the _value_ of the foreign key is updated - cascade the _update_.

I have never needed to use `ON UPDATE` in practice. Presumably this implies a need to _update_ the `id` column (primary key) to an alternative value. `id` columns are usually automatically generated and never need to be changed, but I always include `ON UPDATE CASCADE` for the unlikely event I find myself in that situation.

In code, these cascades look something like this:

```typescript
export class AuthorEntity {
  @ManyToOne(() => PostEntity, (post) => post.author)
  posts!: PostEntity[];
}

export class PostEntity {
  @OneToMany(() => AuthorEntity, (author) => auth.posts, {
    onDelete: 'CASCADE',
    onUpdate: 'CASCADE',
  })
  author!: AuthorEntity;
}
```

Note the cascade configuration is on the child relation, which in this case means when an `author` is deleted, delete this `post`.

### TypeORM Cascades

While also referred to as a "cascade", this actually has nothing to do with database cascades. It is more of a "software cascade". Or, in other words, allows you to insert/update/delete multiple records at once in a single repository call. For example,

```typescript
const author = new AuthorEntity();
author.name = 'Jason';

const post = new PostEntity();
post.name = 'TypeORM Migrations';
post.author = author;

repository.save(post);
```

Normally, this would not create the `author` if it did not already exist. Without cascades you would need to save the `author`, set it on the `post`, and finally save the `post`.

With cascades turned on, TypeORM will do this for you in a single call.

In code, this type of cascade looks something like this:

```typescript
export class AuthorEntity {
  @ManyToOne(() => PostEntity, (post) => post.author)
  posts!: PostEntity[];
}

export class PostEntity {
  @OneToMany(() => AuthorEntity, (author) => auth.posts, { cascade: true })
  author!: AuthorEntity;
}
```

Of course, since these are two completely unrelated functionalities, they can be used independently.

## Conclusion

I know that TypeORM cascades can be confusing, but hopefully this overview has helped clear up common misunderstandings between the two, so that they can be used more effectively in your next project.

[typeorm]: https://typeorm.io/
